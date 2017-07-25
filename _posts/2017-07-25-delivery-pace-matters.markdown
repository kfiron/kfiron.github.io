---
layout: posts
title:  "Delivery pace matters"
date:   2017-07-25 12:38:44 +0300
comments: true
categories:  delivery fast culture
---
<p>
In last 20 years of my career i came across people that told me things like:
</p>
<p>
<i>If you develop fast it means that you don’t pay attention to quality</i>
</p>
<p>
<i>	
You will hit non breakable wall
</i>
</p>
<p>
And more…
</p>
<p>
As big fan of TDD, clean code and great resilient software architecture I can clearly say that those sentences are purely “bullshit”.
</p>
<p>
Fast does not imply that will finish entire project in one month, or to be the most fast coder that love context switch and work until midnight every day.
</p>
<p>
<b>A major tip would be small chunks - but each with great value.</b>
</p>
<p>
Given example of new project that sends SMS server, we obviously need to think of:
</p>
<p>- Domain and API</p>
<p>- Persistence for the messages</p>
<p>- Integration with SMS providers - maybe few of them, per country</p>
<p>- Black list</p>
<p>- Do not disturb</p>
<p>- Backoffice UI application</p>
<p>- Throttling</p>
<p>- Validation</p>

<p>
Only by watching this list we can imagine that it will take 3 months of coding. 
</p>

<p>
The idea is to start with the smallest part that can give the highest value, so i would start with Domain and API + Integration with one generic SMS provider, this chunk gives a real value of deliver product that do the main goal.
</p>

<p>
We can delivery to production this version in 1-2 weeks. After that we can decide if we want to launch this software, maybe we can use it internally.
</p>

<p>
By having this we can also let our clients to start doing integration, this means that if we make great choices we let other people to move fast. We always need to start from things that are blocker for other teams, reducing the dependencies in the organization is crucial.
</p>

<p>
Another great side effect is to get fast feedback from our clients and to make changes along the way before the real launch.
</p>

<p>
Not having small chunks will have bad impact on the entire company, our product managers would be frustrated by waiting 3 months for sometime that might happen. We can get feedback from them every week, and make them get feeling that we moving super fast, even though we spend the same efforts of the developers every day.
</p>

<p>
Fast feedback loop from the audience in the beginning of the project is great also if they don’t like it. We can throw away code that we wrote for 1-2 weeks, we tend to fall in love with big long projects, we already invest 6 months, so we will try to fix our crappy solution to justify our work.
</p>

<p>
Another advantage of small chunk is that soon enough we can recognize that we may need more things to develop and we can hire more developers to help. So we also have fast feedback loop from the organization structure point of view.
</p>

<p>
If you do not find great small chunk with value for a new project, you may have “product smell”, it would be great to describe and share this with the product manager and get his feedback and advice of what would be great to begin with.
</p>
<p>
Summary:
</p>
<p>
Develop fast does necessarily means that your coders in the organization are fast, it means that you choose to slice your project into tiny slices that are deliverable and have real business value, at least from the beginning point of the project.
</p>


