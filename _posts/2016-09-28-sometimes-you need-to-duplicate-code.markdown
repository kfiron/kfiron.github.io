---
layout: post
title:  "Sometimes you need to duplicate code"
date:   2016-09-28 06:38:44 +0300
categories: scala testing code
---

<p>
Yes, code duplication is the first rule to avoid when we try to provide clean code. In this post i will try to show i use case that you need to have a duplicate code, and it is OK.
</p>

# Given following test (specs2)
{% highlight java %}

trait Context extends Scope{
   val usersManager = new UsersManager()
   val userId = "some-id"
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
}

{% endhighlight %}
