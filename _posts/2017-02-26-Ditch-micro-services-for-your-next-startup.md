---
layout: post
title: Ditch Micro Services for your next Startup
summary: Look at the interest grow about micro services. There is a conference dedicated to it, MicroXchg, and I spoke at it[1]. If you are thinking of building micro services I urge you to reason out the complexities involved. If you are starting fresh or are a small team micro services is not the right choice. My retrospect justifies why.
---
	
Look at the interest grow about micro services. There is a conference dedicated to it, MicroXchg, and I spoke at it[1]. If you are thinking of building micro services I urge you to reason out the complexities involved. If you are starting fresh or are a small team micro services is not the right choice. My retrospect justifies why.

![Screenshot Micro Services Trend](/images/others/microservices-trend.png "Google trends on Micro Services.")

In 2015 I joined OptioPay to build a system that transfers money. We had a clean slate to build an API that our UI team would consume. We decided to build it using micro services, this with a team of six.


# Service Decomposition

One of our early challenges was service decomposition. Martin Fowler describes in his article[2] to use bounded context. He summarises what the [] says in his book, the Domain Driven Design[3]. This is the right approach to decompose services. The challenge though is when you are starting a product the domain is not very clear. You learn the natural boundaries by time either through planned experiments or acquired experience.

We got it wrong by choosing to decompose services based on entities. If I were creating a system for a blog engine with entities Article, Comment, Tag and User for each I would have a service. This let us to 73 services of which 41 are API servers. Remember we were a team of six. Decomposing services incorrectly led us to have dependencies between each other. The below image shows dependencies between services.

![Service Dependencies](/images/others/dependencies.png "Service Dependencies")


The problem with dependencies is the tight copuling between them. Adding new functionality affects multiple services. This causes duplication of work because you tend to write similar functionality in dependent services. 

I recommend not to start with micro services because it is difficult to determine the natural boundaries at the beginning. If you are like us, a start-up that is venturing into a new field, you may not have many domain experts. You may gain knowledge of the domain over time.

# Operations

With a monolith you have a few services to monitor, deploy and debug. When things go wrong you know where to look. With usual stack of a database, a queue, a caching system and the process running business logic the number of systems you need to monitor are less. There are different ways to architect how the micro services use the database, cache and the queue. You could share these process across all services or have individual instances for each micro service. Both approaches adds overhead to deployment and debugging. You will have to think a global monitoring system which provides uniform metrics. Logs from all services must be pushed to a centralised system if you want to remain sane. This is quite an overhead when your team is small. I haven't mentioned functionality like load balancing and backups.

Looking through all our tickets on Jira over the last one and a half year I observed 11% of our tasks per week are related to operational tasks. These do not include complexity and duration of each of the tasks. I remember tasks relating to our staging environments dragged for several weeks. Here is a comparision of tasks added per week and ones that relate to infrastructure.

![Number of operational tasks](/images/others/operations.png "Tasks related to operations")


There are some who claim[4] it is better to move complexity to infrastructure tasks as these can be automated. For larger teams with this might work but not for a small team like ours.

There are inherent complexities involving distributed systems that I have not mentioned. I have provided you with two reasons not to do micro services that are relative to the stage your product is at and the size of the team. 


[1] https://www.youtube.com/watch?v=yVUiA6gDhKU
[2] https://martinfowler.com/bliki/BoundedContext.html
[3] Domain Driven Design by Eric J Evans
[4] https://www.oreilly.com/ideas/microservices-shift-complexity-to-where-it-belongs
