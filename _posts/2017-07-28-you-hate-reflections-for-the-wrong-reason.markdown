---
layout: posts
title:  "You hate reflection for the wrong reason"
date:   2017-07-25 12:38:44 +0300
comments: true
categories:  reflection java
---

<p>
We don’t like reflection, we don’t like it because the “main fact” that the performance is lower by order of magnitude. Some optimizations by the JVM cannot be performed using reflection. But it is the most less important reason. Nowadays CPU is fairly cheap, usually our servers are suffering from intensive I/O and not from high CPU consumption.  
</p>

<p>
And don’t get me wrong, we need to think about CPU consumption, it is part of building culture of excellence, but really want to talk about the elephant in the room, but different elephant that sits on the corner and no one see. 
</p>
<p>
<b>	
So why reflections is bad? 
</b>
<p>

<p><b>1. Leaky abstraction</b></p>
<p>
Object has interface (constructor, getters, setters), and this is the only way to access the object. I nice metaphor for object is your home, the access to your home is from the main door. Let’s say that you have open window and people visitors enter your home from the Window. It seems that it will work, it might be strange though, but it will be ok.
</p>
<p>
But what the visitors will lack by using the window to enter your home?
</p>

<p>- They will miss your welcome wall picture on the entrance</p>
<p>- They will miss the place the box that for put the umbrella</p> 
<p>- The window is small and above the floor, so some people might fall and break a bone or something</p>
<p>- Let’s say you have a bell that rings whenever the door is open, like in 7-Eleven in Thailand, you will miss it. </p>

<p>
The same as code, we may have logic inside our getters and setters, and by accessing the values and read/mutate them we let developer to bypass them and access the data like a thief from the window. 
The way we keep the data in our objects is our problem, we want people to access the API.
Few examples:
</p>
<p>
1. We can save date-time as long number internally, but we want people to get Joda-time, or even nicely formatted date string
</p>
<p>
2. Setter for item price, we may decide to add the tax on the setter
</p>
<p>
3. We may want to count the times of reading couple of fields, so we may add a counter on few getters, by accessing it from reflection we may use it.
</p>

<p><b>2. Readability of the code and code flow</b></p>
<p>
Reflection API is kind of meta-programming, the problem with meta programming is that inherently things goes on the background. 
You can think of reflection as a way of letting developer set behaviour on your object but not from the object, from different place. So we can make project manipulation from totally different project and different repository. This imply that it may hard to find it and make changes. One of our main goals in design is be able to find where to make changes.
Flows and logic should be done closed to the object. 
</p>

<p><b>3. Deprecation  support</b></p>
<p>
Accessing methods and properties in reflection are “non-typed”, deprecation of methods and properties will not be reflected at your clients, and you’ll end up keep supporting old non-relevant data. One of other main goals for software engineering is that “Software must evolve".
</p>

<p><b>Summary: Don’t use reflection!</b></p>


