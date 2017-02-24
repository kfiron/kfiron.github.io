---
layout: posts
title:  "Sometimes you need to duplicate code"
date:   2016-09-28 06:38:44 +0300
comments: true
categories: scala testing code
---
<p>
Yes, code duplication is the first rule to avoid when we try to provide clean code. In this post i will try to show i use case that you need to have a duplicate code, and it is OK.
</p>

# Given following test (specs2)
{% highlight java %}

trait Context extends Scope{
   val usersManager = new UsersManager()
   val userId = randomId
   val user  = User(name = userId)
}

"User server" should {
   "login" should {   
     "returns not exist for non existing user" in new Context {
        usersManager.byId(userId) must beNotFound  
     }
     "returns success for existing user" in new Context {
        
        usersManager.create(user) must beCreated
        usersManager.byId(userId) must beUserLike(user)
     }
   }
   "register" should {
    "be created" in new Context {
      usersManager.create(user) must beCreated
      usersManager.byId(userId) must beUserLike(user)
    }
  }
  "delete" should {
    "beDeleted" in new Context {
      usersManager.create(user) must beCreated
      usersManager.delete(userId) must beDeleted
      usersManager.byId(userId) must beNotFound
    }
  }
}

{% endhighlight %}

<p>
Obviously, we have code duplication in usersManager.create() and usersManager.byId(), let's look in example of this code when we get rid of all code duplications
</p>

{% highlight java %}

trait Context extends Scope{
   val usersManager = new UsersManager()
   val userId = randomId
   val user  = User(name = userId)
   def givenUser = usersManager.create(user)  
   def login(userId: String = userId) = usersManager.byId(userId)
   def verifyUserCreated = login(userId) must beCreated
}

"User server" should {
   "login" should {   
     "returns not exist for non existing user" in new Context {
        login must beNotFound  
     }
     "returns success for existing user" in new Context {        
        givenUser must beCreated
        login must beUserLike(user)
     }
   }
   "register" should {
    "be created" in new Context {
      givenUser must beCreated
      login must beUserLike(user)
    }
  }
  "delete" should {
    "beDeleted" in new Context {
      givenUser must beCreated
      usersManager.delete(userId) must beDeleted
      verifyUserCreated must beNotFound
    }
  }
}

{% endhighlight %}

<p>
The problem with this code that we hide the API, the tests are the documents for our code, when someone opens your code and for example look at the login section he wants to undesrtands how to tirgger login, and he does not wants to follow the abstraction you created to avoid duplications.
And definitely on tests that uses the login for verification that user is created then we need to see the semantic of the verficication.
Also for tests that test the login we do want to see the semantics that user is created, and in this case we don't care how. So let's see a proposed solution
</p>

{% highlight java %}

trait Context extends Scope{
   val usersManager = new UsersManager()
   val userId = randomId
   val user  = User(name = userId)
   def givenUser = usersManager.create(user)  
   def verifyUserCreated = login(userId) must beCreated
}

"User server" should {
   "login" should {   
     "returns not exist for non existing user" in new Context {
        usersManager.byId(userId) must beNotFound  
     }
     "returns success for existing user" in new Context {        
        givenUser must beCreated
        usersManager.byId(userId) must beUserLike(user)
     }
   }
   "register" should {
    "be created" in new Context {
      usersManager.create(user)  must beCreated
      usersManager.byId(userId) must beUserLike(user)
    }
  }
  "delete" should {
    "beDeleted" in new Context {
      givenUser must beCreated
      usersManager.delete(userId) must beDeleted
      verifyUserCreated must beNotFound
    }
  }
}

{% endhighlight %}

# So now we have 2 types of code duplications:
* The login uses byId twice, because it is the API for this tests and we don't want to hide it
* The abstractions verifyUserCreated/givenUser is hide the API, which we are using in the same file. but we can use this abstraction in more tests in future.
