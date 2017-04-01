---
layout: posts
title:  "Either monad for node.js"
date:   2017-03-25 12:38:44 +0300
comments: true
categories:  nodejs monad either
---
<p> 
Sometimes you have a function that may return either of completely different object types. for example login() function may return the user information or an error object.
Either to the rescue! It let's you return either or left which are from type of Either. And then you can decide what to do based on the left/right existence.
I just wrote a node.js library for that, the library have built from insparation i got from Scala either monad. 
</p>
[node-either-monad](https://www.npmjs.com/package/node-either-monad)

<p>
Enjoy :)
</p>

