---
layout: post
title: Solve the right problem
---

When I was a kid every day was interesting, at least the ones that did not have tests. Packing boxes were flying machines and race cars; a tyre and a stick were a motorbike; life was simple. Somewhere I seem to have lost that ability to keep things simple. For most of my life as a software engineer I have found ways to make simple things complicated, or worse, trying to invent problems to solve.

Reading blog posts and watching talks at conferences I felt inspired to introduce a new technology into a system that clearly didn’t need it. At a previous job, we built an entire project using event sourcing and microservices. Was it necessary? Absolutely not. But partly we chose to do it as it was an "interesting way" to solve the problem. By doing so we introduced problems of a distributed system and a high complexity of managing the infrastructure. 

I am reminded of the principal-agent problem[1]. The dilemma is that agents are motivated to act on their own interests, which are contrary to those of their principals. This problem is observed with politicians and voters, lawyers and clients, and brokers and sellers. At times it can be observed with software engineers and their employers. By introducing microservices to an organization that clearly doesn’t need it, the engineer(the agent) is acting in her own interest; a feather in her cap for the next job. 

As software engineers it is our responsibility to understand the problem at hand and solve it as simply as possible. Most of the times it will not be Google scale problems and that is okay. Hopefully we solve the problem right and the company grows to the scale of Google. There are definitely others at fault, sales tries to sell us a vision of millions of users; but we need to strain out the facts. 

Understand the domain is key to solving the right problem. Eric Evans, in his book Domain Driven Design, provides enough material to help you with this. Instrumenting for observability is another way to ensure you solve the right problem. Adding metrics to your services and contextual logging help you understand your system better. If you see a growth in the number of requests, plot a graph and see if you will be able to handle requests in the near future. Instrument the process of development. This way you can validate if there is a need to split into microservices. 

This is more a note to my future self to ensure I don’t get carried off by an inspiring video of Netflix using "tumultuous baboon" to ensure fault tolerance for their drones.

1. [Wikipedia article on Principal-agent problem](https://en.wikipedia.org/wiki/Principal%E2%80%93agent_problem)
