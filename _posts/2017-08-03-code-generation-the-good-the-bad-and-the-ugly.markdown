---
layout: posts
title:  "Code generation - the good, the bad & the ugly"
date:   2017-08-03 12:38:44 +0300
comments: true
categories:  reflection java
---

<p>Code generation is something we tend to do for years in some cases:</p>

<p>1. Protocol generation when we have deterministic logic, for example generation of stubs from IDL/Schema (CORBA, Soap, gRPC)</p>

<p>2. Boilerplate projects - Using Yeoman generator, it is much familiar in frontend project when we need to craft together many tasks like transpiling, minifying.. Etc</p>

<p>3. Macros are programmatic code generation, even in C++ when we use #define, we use it as a function and the result will be written as code on build phase. </p>

<p>4. I even saw cases where people generates code from UML. Luckily it was very long ago in late 90s.</p>

<p><b>The good:</b></p>

<p>In some cases code generations comes to improve our velocity and to hide our pain. It makes our life easier. </p>

<p>In the IDL use case, it hides the pain of generating structs and buffers. And we let the user to use the most fundamental way to use the protocol by only creating new objects and calling methods.</p>

<p>In boilerplate project, we increase the development velocity, developer does not need to remember how to set the linter, how to wire the beans into the infrastructure and so. And as we use more and more tools we just add them to the boilerplate projects and people just get it.  </p>

<p>Around 10 years ago i was involved in a project written in C++, The server exposed TCP/IP interface which defined in “.h” file made of multi dimensional structs, so we wanted to have top layer Restful (It was not called Restful on that days) Api, so we did some code generation from the C++ header file into Java implementation using NIO, it was pretty cool and we were able to increase velocity and exposed more and more deep granular API without changing the core server.</p>


<p><b>The bad:</b></p>

<p>Boilerplate project is evolving inherently, but old clients cannot get the changes, the boilerplate generators are good for projects that are new. And it is purely code duplication, strict violation of DRY with all meaning. If we introduce bug in the boilerplate generator the bug will be reproduced in every language. </p>

<p>Another problem with kind of projects, it sometimes not clear enough where is the generated code and where is the customized code per project. </p>

<p>For IDL based code generation, the generated code might also introduce code duplication, sometimes bad naming, it is not fun to debug into generated code with bad names. And when we generate code we want to support plenty of functionality, so sometimes those libraries generate a lot of noise when we want to solve small problems. </p>

<p>Also due to the fact that it is kind of meta programming, it is much harder to apply good design principles. </p>

<p><b>The Ugly:</b></p>

<p>In boilerplate project developers gets high velocity, they run single command line and the get full blown project, the downside is that developer treat is as black box and it will be harder for them to learn and deep dive into the internals. It is a mgic. </p>

<p>Another compelling reason for the ugliness is the fact that with boilerplate we hide the pain of complexity for wiring the application, and it is big smell, and by that reason we will not find time to fix the infrastructure, because it is “not painful” anymore.</p>

<p><b>Summary:</b></p>
<p>Development velocity is crucial, we need to be fast and sharp, react to pain and hide it as long as we understand that boilerplate projects are smell that our library need to be more simple. </p>
