# Chapter 13 & 14

## Service-Based Architecture Style
“A solid, general DDD style. It's the simplest of the distributed architectures. Topologically it looks like a meatball sandwich.”

**Topology:** A distributed macro-layered structure. A presentation layer interacts with 4-12 coarse grained services, which in turn interact with 1 centrally shared database. (The number of services tend to be limited by the single DB.) While multiple instances of each service domain can be scaled up, typically only one instance exists. Because they are coarse, each domain is often further subdivided into layers or domains. The single database enables SQL joins and queries like you would in a monolith. Many topology variants can be imaged: FE per service, DB per service, API layer.

A note on DB organization: having a single shared library is probably the least effective. More effective is to logically partition into fine-grained domains so the services only rely on a subset, and changes to the DB only affect a subset.

Two service designs: 
direct access design: each module exposes a RESTful endpoint that the API layer accesses.
API access design: there’s and API access facade that injects the modules that allows separation of concerns and protocol agnostic processing.

**Partitioning:** Domain

Pros:
- A good initial default that can be broken into small services as the app grows
- Better time to market: faster changes and testing means service deployments have less risk
- Good fault tolerance: if one service goes down others are not affected
- Preserves ACID transactions better than other distributed architectures

Cons:
- Tends to have more duplication than micro services due to coarse grained nature of the services.

### Q&A with Bert

Service oriented is a good fit for the vast majority of people. There’s a range from monolith to completely distributed. There’s a long tail of companies that should be, at maturity, still a monolith. Most organizations fall in the middle of the bell curve and the service-based, with its coarse grains, tends to serve the middle of bell curve very well. People who lean into this style often feel the friction of a monolith. Scalability is a false flag, the real problem is often low cohesion high coupling where you end up breaking things unintentionality. This is the one architecture style that business has the right intuition about when they think about how they architecture works. Usually there’s a business and tech divide, but both mental models tend to align well with this style. The bottleneck the gets exposed with this architecture style is the DB, which led in part to new patterns in noSQL use.

How to break into coarse grains: Eric Evans wrote an under appreciated book that is highly quoted and poorly read, “Domain Driven Design”. Everyone’s read about it through another book. For a summary of DDD read San Newson. His approach is “half of Bert’s” answer. With monoliths everything is one context. DDD gives the idea of a bounded context. Service is a continuum on the point to micro services. A monolith, everything is in the same context. With micro services you’re aiming for the smaller possible bounded context. They tend to be around specific actions. Most people will judge you for RPC, but it is useful in the MS context because it is about control over specific actions. What Eric’s book does is give a proper definition of a bounded context. The context is usually around specific capabilities. As soon as you can make a distinction around a business function you can usually draw a line.

Once you have over a certain number of services you end up in the microservice world.

The way we typically ensure transactions is through two phase commit, like git. You git add, and you git commit. Git stole this model. That’s the principle of ACID transaction. It’s possible with services but not advisable because you’d have to lock your system. It’s one thing with a monolith but another with a distributed system. There’s a saga pattern popularized by Twitter. It was invented by academics. They also popularize snowflake. The ability to get a unique value in a distributed system. Every tweet is giving it’s own value. The saga is usefule where every micro service write would be uncoordinated, think Expedia where’s there independent booking services: plane, car, hotel. If one fails it needs to send an undo message to the others. The actions need to be append only, and very reversible.

## Event-Driven Architecture Style
“For complex and dynamic workflows in response to some initiating event. There are two variations: broker a.k.a fire and forget, and mediator, a.k.a central command.”

**Topology:** Where a “request” model is synchronous and deterministic, an event-based model reacts to a particular event in 1-n different ways. There are two main topologies: broker and mediator.

**Broker:** “An uncontrolled chain reaction”. messages flow through a lightweight broker like RabbitMQ. Messages are advertised and event processors react to the event and publish new events when complete. The process continues until no one is listening anymore.

Pros:
- Each event processor can be scaled independently.

Cons: 
- Fragmentation into event processors reduces overall visibility into the system.
- If a failure occurs no one is aware of it or handles it.

**Mediator:** “A centrally managed message delivery”. Multiple mediators maybe involved. The event processor always communicates back to the mediator who decides what to do next. The mediator can take a corrective action if there’s a failure. Note that not all events/processors are the same and have different complexities that should impact the decision of which tech to use for the central mediator.

Pros:
- Visibility into the system and failure handling

Cons:
- Less scalable, performant
- More complex workflow modelling
