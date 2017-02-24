---
layout: posts
title:  "Don't abuse JSON with frameworks"
date:   2017-02-24 12:38:44 +0300
comments: true
categories:  frameworks json magic software engineering java
---
<p>
Who does not love JSON? nowadays json is defacto transport representation for payload of Ajax APIs, As well for Rest calls from server to server. it is almost native from Javascript in the client side, it is kind of compact (in comparison to XML), it is readable for human being - easy to debug (No need to decode/decrypt.. etc), it also descriptive and it helps your API to be self explains (in comparison to binary protocols".
</p>
<p>
There are tones of libraries that hadles JSON in the JVM ecosystem. The most intuitive thing I am thinking of when i want to read json is to represent it as AST, and be able to "swim" between the elements and read them by name. To be more correct it is an AST for deterministic list of types: String, Int, null, boolean, Object(which contains the primitives and or more objects)
</p>
<p>
The problem is that develoeprs trying to be too smart, and trying to make our life easier, they thinks that they can make our life aasier.  
</p>

#  given the following json for users api
{% highlight json %}

    { 
      "name": "Kfir Bloch",
      "email": "i-will-not-tell-you@go-to-hell.com",
      "age": 40
     }
      
{% endhighlight %}

<p>
Let's take a loot at Jackson (One of the most common libraries in JAVA), it has option to give the library the stream of data and get a class that represents the fields by name
</p>

{% highlight java %}

 class User {
   private String name;
   private String email;
   private int age;
 
  // getters and setters
 }

 ObjectMapper mapper = new ObjectMapper();
 User user = mapper.readValue("{Json... }, User.class);
{% endhighlight %}

<p>
Even Spring (Which i am sure you hate - and if you don't ask me why) has the capablity to let you read parameters from controller as object which are mapped from JSON, as well using Jackson by default
</p>

{% highlight java %}

 @Controller
@RequestMapping("/api", RequestMethod.POST)
 class UserController {
    @RequestMapping("/post-user", RequestMethod.POST)
    public Result postUser(@RequestBody User user){
      // user use to be a json
    }
 }
{% endhighlight %}


<p>
Looks awesome, now all i need to do it to create a class and BOOM, i have this magic. BUT... Like any other goodies, it has its tradeoffs:
</p>
* If we want different name for our domain object from the one in the json (because javascript developer likes undescores), yes we can pollute the class and annotate. 
* Let's say that are getting more parameters, JSON breaks (yes we can annotate here - @IgnoreUnknown, pollute the domain again
* This approach natively leads towards leaky abstraction, where the object from the transport being used in our internal core services. Yes, we can create transformers, but developer can make this mistake.
* Jackson support custom ser/deser handlers, so different users can treat different complex object differently on the transport. We using the class as our IDL, but since this IDL does not contains only primitives it may be not be read properly between different clients/servers. For example Scala Enumaration by default ser to an object with few properties. Now let's explain this to the client developers, he now need to care about different acosystem? All they asked is to pass a json which is an object that may contains another object that may contains some primitives.
* Custom ser/deser are hidden, you hide the most important part of your application, you hide the way your application is talking to another system. I want to see on a single place how my object model transforms into a JSON, this is my contract to with the world.

<p>
I want to tell you that are not using JSON! You are using framework that gives you nice hello-world capability, you are getting out of the box a magic, which you will pay in future as long as the APIs and the domain evoloves. <B>You are violating the basic rule of separation of concerns</b>. A parser is something that does parsing, and a domain object is object that you use in your services to represent info. Don't combine them.
</p>
<p>
Let's say i am reading an existing API and i care only about name and email
</p>

{% highlight java %}

   class UserInfo {
     // my domain
     public UserInfo(String name, String, email){
         
     } 
   }

   JsonNode json = mapper.readTree("{Json..."});
   UserInfo userInfo = new UserInfo(mapper.get("name").asText(), 
                                    mapper.get("email").asText());


{% endhighlight %}
Benefits:
* UserInfo is only your domain, it is OK to pass it along in your application and services.
* You know the json, you read the fields by their names, not projecting the json to names by class members implicitly.
* The domain object is not polluted with annotations
* You don't have custom hidden ser/deser handlers, when other developers reads the code, it will be easy for them to see it in a single place how domain transforms to a json and vice versa
* Performance wise? in some json implementations, becasue mapping JSON to object in a magic manner sometimes being done by reflection.

<B> You want JSON, use JSON!<b>
