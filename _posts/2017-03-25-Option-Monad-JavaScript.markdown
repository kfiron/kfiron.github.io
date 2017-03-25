---
layout: posts
title:  "Using Option Monad with JavaScript"
date:   2017-03-25 12:38:44 +0300
comments: true
categories:  nodejs monad option
---
<p> 
Option monads comes from functional programming world, it helps to resolve if object is null or it has data. 
By having such semantic we can do some declarative APIs like forEahc/Map/Fold... etc.
It makes our program more readable.
</p>
<p>
I have creates open source project for node.js users: 
</p>
[scala-like-option](https://www.npmjs.com/package/scala-like-option).
<p>
However when I published it a lot of develoeprs told me that this is not idiomatic way to handle nulls in Javascript in declarative manner.   
</p>
