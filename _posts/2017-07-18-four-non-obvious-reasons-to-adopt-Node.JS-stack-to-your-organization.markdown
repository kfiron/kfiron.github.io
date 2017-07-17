---
layout: posts
title:  "4 non-obvious reasons to adopt Node.JS stack to your organization"
date:   2017-07-18 12:38:44 +0300
comments: true
categories:  nodejs
---

<p>
You may heard about node.js, It is great tool for heavy I/O due to the fact that it is async by nature. It also has nice capabilities such as server side rendering using React+Redux and of course the overrated buzz around isomorphic code. But i don't want to talk about all that, 
let's see some more compelling reasons to adopt it in your organization.
</p>

<p>
Before that a disclaimer: I am Scala/Java developer & I love the type system and still think that there are cases only for statically typed languages.
</p>

<p>
<b> 1. Fast feedback loop in development phase </b>
</p>
<p>
As Scala/Java developers we are facing low feedback loop in development, compiling on each change to a file, and JVM load slowly, building the classpath, sometimes we are using things like Spring with bean scanning and unfortunately we sometimes using classpath scanning. By doing TDD we need to recompile the project every time we run the tests and running heavy http container. 
</p>
<p>
While working with Node.JS i found myself very productive, because the fact that full test suite with 100 tests that each of them run new server takes less than a minutes.
</p>
<p>
We can use much leaner containers and framework and we can gain better results, but in the end it is different by order of magnitude.</p>
<p>
<b>2. Extendable language</b>
</p>
<p>
Javascript supports transpiling, the transpiling is nice because we can use different code with many features which improve readability and velocity. On the transpiling phase the javascript converted into AST and then transpiled into language that can be interpreted by the runtime. We can even use TypeScript if we care about the types and interfaces we exposing in the API.
</p>
<p>
And we even can create our own transpilers and support our own language features.
</p>
<p>
<b>3. Large ecosystem, rich open source libraries</b>
</p>
<p>
Again we want to gain velocity, we don't want to reinvent the wheel over and over again. The node.js library ecosystem (NPM) contains 500K packages of open source project that created by the community. We can find almost everything we can dream of.
</p>
<p>
And of course it is fairly easy to contribute, with simple command line (npm publish) your package to npmjs.com, which is awesome.
</p>
<p>
<b>4. Your frontend developers already knows javascript</b>
</p>
<p>
I believe about expertise of backend and expertise of frontend. Totally different paradigm. Having said that does not imply that frontend developer is not allowed to make modification to the server and vice versa. 
Having node.js on the server soften the boundary, and let the frontend developer lower learning curve of the server paradigm. 
</p>
<p>
It will be great that in small teams of 2 backend and 2 frontend everyone will able to do everything, or at least be able to get help from all team members in all application layers. 
</p>

