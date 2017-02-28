---
layout: post
title: Ditch Micro Services for your next Startup
summary:
---
	
Look at the interest grow about micro services. There is a conference dedicated to it, MicroXchg, and I spoke at it[[1](#2)]. If you are thinking of building micro services I urge you to reason out the complexities involved. If you are starting fresh or are a small team micro services is not the right choice. 

![Screenshot Micro Services Trend](/images/others/microservices-trend.png "Google trends on Micro Services.")

In 2015 I joined OptioPay to build a system that transfers money. We had a clean slate to build an API that our UI team would consume. We decided to build it using micro services, this with a team of six.


### Service Decomposition

One of our early challenges was service decomposition. Martin Fowler describes in his article[[2](#2)] to use bounded context. He summarizes what Eric Evans says in his book, the Domain Driven Design[[3](#3)]. This is the right approach to decompose services. The challenge though is when you are starting a product the domain is not very clear. You learn the natural boundaries by time either through planned experiments or acquired experience.

We got it wrong by choosing to decompose services based on entities. If I were creating a system for a blog engine with entities Article, Comment, Tag and User for each I would have a service. This let us to 73 services of which 41 are API servers. Remember we were a team of six. Decomposing services incorrectly led us to have dependencies between each other. The below image shows dependencies between services that run on production.

![Service Dependencies](/images/others/dependencies.png "Service Dependencies")


The problem with dependencies is the tight coupling between them. Adding new functionality affects multiple services. This causes duplication of work because you tend to write similar functionality in dependent services. 

I recommend not to start with micro services because it is difficult to determine the natural boundaries at the beginning. If you are like us, a start-up that is venturing into a new field, you may not have many domain experts. You may gain knowledge of the domain over time.

### Operations

With a monolith you have a few services to monitor, deploy and debug. When things go wrong you know where to look. The number of systems you need to monitor are substantially less. Micro services adds overhead to deployment and debugging. You will have to think a global monitoring system which provides uniform metrics. Logs from all services must be pushed to a centralized system if you want to keep your sanity. What about load balancing? This is quite an overhead for a small team.

Looking through all our tickets on Jira over the last one and a half year I observed 11% of our tasks per week are related to operational tasks. These do not include complexity and duration of each of the tasks. I remember tasks relating to our staging environments dragged for several weeks. Here is a pattern of tasks that relate to infrastructure added.

![Number of operational tasks](/images/others/operations.png "Tasks related to operations")


There are some who claim[[4](#4)] it is better to move complexity to infrastructure tasks as these can be automated. For larger teams with this might work but not for a small team like ours.

I have provided you with two reasons not to do micro services for your next start-up. The talk[[1](#1)] I gave at MicroXchg 2017 discusses a bit more about the same topic. My hope is that you learn from our mistakes. 

---

<p><a name="1" href="https://www.youtube.com/watch?v=yVUiA6gDhKU">1.
Complexities of micro services and event sourcing</a></p>
<p><a name="2" href="https://martinfowler.com/bliki/BoundedContext.html">2. Martin Fowler on Bounded Context</a></p>

<p name="3"><a rel="nofollow" href="https://www.amazon.de/gp/product/0321125215/ref=as_li_tl?ie=UTF8&camp=1638&creative=6742&creativeASIN=0321125215&linkCode=as2&tag=satranin-21">3. Domain-Driven Design: Tackling Complexity in the Heart of Software</a><img src="http://ir-de.amazon-adsystem.com/e/ir?t=satranin-21&l=as2&o=3&a=0321125215" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" /><p>

<p><a name="4" href="https://www.oreilly.com/ideas/microservices-shift-complexity-to-where-it-belongs">4. Shift complexity to where it belongs</a></p>
