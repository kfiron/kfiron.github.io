---
layout: post
title:  "Dont' abuse json with frameworks"
date:   2017-02-24 12:38:44 +0300
categories:  frameworks, json, magic, software engineering java
---
<p>
Who does not love json? nowdays json is the defacto transport representation for payload of Ajax APIs. it is almost native from Javascript in the client side, it is kind of compact (in comparisson to XML), it is readable for human being - easy to debug and see the usage, it also descriptive and it helps your API to be self explains (in comparisson to binary protocols".
</p>
<p>
There are tones of libraries to hadle json from the JVM ecosystem. The most intuitive thing i am thinking of when i want to read json is to represent it as AST, and be able to "swim" between the elements and read them by name.
</p>
<p>
The problem is that develoeprs trying to be too smart, and trying to make our life easier, they thinks that they can make our life aasier.  
</p>

#  give the following json for users api
{% highlight javascript %}

    { 
      "name": "Kfir Bloch",
      "email": "i-will-not-tell-you@go-to-hell.com"
      "age": 40
     }
      
{% endhighlight %}

<p>
Let's take a loot at Jackson, it has option to give the library the stream of data and get a class that represents the fields by name
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
Looks awesome, now all i need to do it to create class and BOOM, i have this magic. BUT... it comes with problems
# If we want different name for our domain object from the one in the json (because JS developer likes undescores), yes we can polute the class and annotate
# If we are getting more parameters, JSON breaks (yes we can annotate here - @IgnoreUnknown, polute the domain again
# This kind of approach natively takes us towards the approach that this class will be used as our internal domain and will leak into our core services. Yes, we can create transformers, but developer can make this mistake.
# Jackson support custom ser/deser handlers, so different users can treat different complex object differently on the transport. We using the class as our IDL, but since this IDL does not contains only primitives it may be not be read properly between different clients/server. For example Scala Enumaration by default ser to an object with few properties. Now let's explain this to the client developers, he now need to care about different acosystem?

</p>
<p>
Let's me tell some something, you are not using JSON! You are using framework that gives you nice hello-world capability, you are getting out of the box a magic, which you will pay in future as long as the APIs and the domain evoloves.
</p>
<p>
Let's say i am reading existing API and i care only about name and email
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
* UserInfo is only your domain, it is OK to pass it along in your application and services
* You know the json, you read the fields by their names, not projecting the json to names by class members
* The domain object is not poiluted with annotations
* You don't have custom hidden ser/deser handlers, when other developers reads the code, it will be easy for them to see in single place how domain transform to json and vice versa
* Performance is improving, in some json implementations, becasue mapping JSON to object in a magic manner sometimes being done by reflection.

