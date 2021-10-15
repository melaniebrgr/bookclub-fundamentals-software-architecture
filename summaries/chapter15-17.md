# Chapter 17

## Space-Based Architecture
“A style for dramatic swings in concurrent users”

**Topology:** Most application architectures eventually lead to a performance bottleneck at the database level, which is the hardest thing to scale. The spaced-based architecture style is specifically designed to address scaling, elasticity and concurrency issues. There are several different pieces to the overall topology:
- Processing unit (PU): holds the business logic components, front end and backend apparently, an in-memory data-grid, and an engine to replicate the data between the PUs. PUs are “identical” instances of each other.
- Virtualized middleware: holds a message grid that responsible for forwarding a message to a PU; a data grid that knows about each PU and works with the replication engines in the PUs to keep data in sync; an optional processing grid that mediates between different types of PUs if necessary for a request; and finally a deployment manager that manages the on demand start up and shut down of the PUs.
- Data pump: asynchronously pumps data from the in-memory PU caches to a data writer and the database, providing eventually consistency.
- Data writer: Knows how to update the database, it can be responsible for a domain or a PU.
- Data reader: Knows how to read from the database. It’s only necessary when redeploying all PUs (of the same type). The data writer and reader together form a data abstraction layer.
The reduced dependency on a database is what enables the high scalability, elasticity, and performance of space-based architectures. The tradeoff is the chance of data collisions when PUs replicate data. It is particularly not suitable for huge data sets that replicate frequently.

**Partitioning:** domain and technical

**Example:** online auction system

Pros: scales well
Cons: is complicated, expensive and hard to test

## Orchestration-Drive Service-Oriented Architecture (OD-SOA)
“A historically significant but failed style.”

**Topology:** Layers:
- Business services layer: simply the entry point for each domain, no logic.
- Enterprise services layer: the “atomic”, “reusable” building blocks of all services. This was they key point of failure with this architecture. The dynamic nature of reality defies treating business components like construction material.
- Application services: one-off services used by the enterprise services.
- Infrastructure services: operational cross-cutting services likes monitoring, auth
- Enterprise service bus: integrates the business and enterprise services, becoming the defacto point of political power.

**Partitioning:** Technical

**Example:** Old enterprise apps

Pros: 
Cons:
- Building systems for reuse incurred high degrees of coupling.
- Domains were spread thinly throughout the layers.

## Microservices Architecture
“A currently very popular style invented by Martin Fowler”

**Topology:** Functional decomposition of an application. Microservices is inspired by DDD’s concept of the bounded context. They contains everything it needs to operate and are independently deployable. Coupling is reduced by intentionally minimizing reuse. The granularity of the “microservice” is hard to get right and should be guided by purpose (cohesion), transactions, and communication frequency. Microservice does not means small. Pieces to the topology:
- The (micro) services, which “sidecar” in cross-cutting operational concerns like monitoring and logging are controlled via a service mesh a.k.a operational coupling
- An optional API layer, which should not contain any orchestration/mediation logic
- The frontend can be a monolithic UI or with microfrontends

Each microservice should be able to call another, conveniently following the same standard, and may use a different technology stack, i.e. one better suited to the domain. If a user request relies on more than one microservice a broker or mediator event style approach can be followed, with different tradeoffs. Transactions should be avoided if possible, by fixing granularity.

**Partitioning:** Domain

**Example:** GitHub, Netflix, Amazon, Ebay, Soundcloud, Yelp, Uber

Pros: Modular, deployable, evolvable
Cons: Complexity, cost and performance

### Q&A with Willian
There are a couple reasons Willian is wary of microservices. There is no agreement about what it is. There is a battle between Martin Fowler, Sam Newson and other folks who are the inventors of microservies. The book aligns with Fowler’s viewpoint and it is the closest and best description. The concept of microservices is a reaction to the SOA pattern (the opinionated version of serviced-based in the book). Microservices is the opposite of the prescriptive SOA approach. With microservices you can do whatever you want and just combine them. You can communicate over different protocols. When we see diagrams microservices in the wild though, it’s always a mess of services. The only thing that is common is that each has access to a single database. There is a reason for this: DDD tells us that we should model software based on real life. In that case, when defining boundaries, you're saying that a unique team will control the boundaries of the service. That is the main benefit: it give teams freedom to work independently. Which is also a clue of when we should use them. They are good for bigger teams only. For small teams there is no point. Microservices is also a bad idea if you do not know the business requirements or it's a greenfield project. People tend to think that because they are small things you can have a very performant system, but in general you’re going to add a lot of overhead in terms of communication, as services need to talk to each other.

Another challenge of microservices is traceability. The "sidecar", or sharing things, is generally very against the idea of microservices. Changing one service should not break another. The sidecars, the code that “should be shared” between microservices for traceability should not affect the actual functioning of the microservice at minimum.

When to transition to a microservice architecture? You reach a point where the monolith is blocking development, that is the great time to consider the jump to microservices. Or if you have a long deployment. There is a ton over material on how to address database sharding when taking monoliths to microservices for instance. Build the monolith, feel the pain of it, understand your business domain, then go to microservices.

If you need to talk to multiple services you must have something like a saga or mediator/circuit breaker. The issue then is that the two services are coupled with a mediator or saga. You only do sagas if you need to cancel something given a failure of something else. A saga owns the whole process. In some cases you may not need both service calls to be successful. If the front-end is graphQL, then you can just request the data from the service again. 
