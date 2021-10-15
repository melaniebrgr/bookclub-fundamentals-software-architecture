# Chapter 8 & 9

Chapter 8 discussed components, the pros and cons of different top-level partitioning, and how to approach designing the components of a system. Chapter 9 discussed the pros and cons of monolithic and distributed architectures.

## Components
If modules are collections of related code, a component, in the authors view, is the "physical manifestation", or concrete packaging of a module, e.g. the distributable, deployable, compile-time dependency such as a node module. A component is at a higher modularity level than classes and generally wrap several. A service is a type of component that communicates via a networking protocol or REST. 

### Architects identify partitioning to help identify the components
One of the “fundamental differences between architecture patterns is which top level partitioning it supports”. Any type of partitioning can be imagined, but there are two common patterns: technical and domain top-level partitioning. Note, partitioning often reflects organizational structure (Conway’s Law) and cross-functional teams can be intentional built in what is known as the inverse Conway maneuver. 

In technical partitioning the functionality is organized by technical capability: presentation, business rules, services, and persistence layers similar to the MVC design pattern. Typical software development workflows require developers to work across all the layers at once.

Domain partitioning is inspired by Eric Evan’s “Domain Driven Design” (DDD). The goal there is to identify domains or workflows that are decoupled for each other. Each domain could have it’s own db/persistence layer.

Question: Technical partitioning and monolithic, and domain partitioning and distributed seem to go together, but are not locked in. Is it possible to have technical layers and be distributed system, or have domain partitioning and be monolithic?

### Architects identify the components
Partitioning of components in the architecture is one of the first and primary decisions an architect must make. To identify components, they need to know how to partition architecture.

### Component identification is iterative:
1. Map domain functionality/behaviour to an initial set of components. The goal is to partition the domain into coarse chunks. There are different analysis strategies:
    1. Actor/actions approach: actors and the actions they take are identifies
    2. Event storming: events that occur in the system are identified and components are built around those events and message handlers (suitable for micro service architectures)
    3. Workflows approach: what are the workflows the key roles engage in
2. Align requirements to components and adjust as needed
3. Align roles to components and adjust as needed
4. Analyze architecture characteristics for components and adjust as needed
5. Iterate in collaboration with developers as development progresses 

No component design will be perfect, try to find the least worst one.

### Monolithic vs. Distributed
Distributed architectures are more efficient in terms of performance, scalability and availability. Monolithic are more efficient in terms of complexity, e.g. logging, monitoring, data consistency and integrity. Distributed systems are not always better. Here are 8 fallacies of distributed systems:
1. The network is reliable: the more a system relies on the network the less reliable it is
2. Latency is zero: inter-component communication time is a monolith will always be smaller
3. Bandwidth is infinite: inter-service communication may cause the network to slow down, especially if there is “stamp coupling”
4. The network is secure: surface area of attack is greater in distribute systems, every endpoint needs to be secured.
5. The topology never changes: network admins are constantly making changes
6. There is only one admin: greater communication between more people is required
7. Transport cost is zero: infra costs are greater
8. The network is homogenous: some network hardware don’t integrate well together
