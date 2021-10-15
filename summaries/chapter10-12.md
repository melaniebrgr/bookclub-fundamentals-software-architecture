# Chapter 10

## Layered Architecture Style
“The cheap, quick and easy way to work. Often the default. If layers aren’t enforced it can turn into a ball of mud”

| Architecture Style | Layered |
| ------------------ | ------- |
| Partitioning type | Technical |
| Number of quanta | 1 |
| Deployability | ⭐ |
| Elasticity | ⭐ |
| Evolutionary | ⭐ |
| Fault tolerance | ⭐ |
| Modularity | ⭐ |
| Overall cost | ⭐⭐⭐⭐⭐ |
| Performance | ⭐⭐ |
| Reliability | ⭐⭐⭐ |
| Scalability | ⭐ |
| Simplicity | ⭐⭐⭐⭐⭐ |
| Testability | ⭐⭐ |

**Topology:** Components are organized into horizontal layers, commonly presentation, business, persistence, and database. The layers of the architectures aren’t necessarily deployed together, e.g. presentation, business and persistence is commonly deployed separately from the database layer. Layers can be closed or open. A closed layers means the layers above and below are isolated from changes to each other, enabling them to be swapped. It is important to document and enforce which layers are open, closed and why or tightly coupled components can result from inappropriate layer access. Domain logic tends to get spread through each layer.

**Partitioning:** technical

Pros:
- A good starting point when the architecture style is still undecided
- Good for short timelines and tight budgets
- Ideal for small, simple applications
- Devs with a specific skillset can be immediately productive
Cons:
- Tends to reinforce a particular skillset, limiting growth
- Lowered agility due to reliance on others to complete features
- Can be difficult to make changes that impact only a single domain since domains are spread through the layers
- Can result in “architecture sinkholes” where most data is simply passed through with no transformation (20% straight pass through is fine)
- Does not age well: tends towards a ball of mud
- Distributed as a monolith, it has the same limitations of monoliths: low fault tolerance, low scalability, low elasticity

## Pipeline Architecture Style
“Simple but powerful composable components. Ideal for processing tasks”

**Topology:** Components are organized into a serial, one-way, bucket brigade of pipes and filters. Filters are stateless, ideally single purpose, operations carried out on the payload that is piped between them. Modularity emerges from the compositional nature of the filters. The pipes are the communication channels between the filters. There are four common categories of filters: producer, transformer, tester (conditionally outputs), and consumer.

Question: The authors describe this as a monolithic style, is there no scenarios where segments of the pipeline are deployed separately?

**Partitioning:** technical (partitioned into filter types)

**Example:** ETL (extract, transform, load) tools, shell scripts

Pros:
- Simple to understand and low cost
- Ideal for one-way processing tasks
Cons:
- Distributed as a monolith, it has the same limitations of monoliths: low fault tolerance, low scalability, low elasticity

## Microkernel Architecture Style
“A core system that can have any number of components plugged in to provide optional, additional functionality.”

**Topology:** The core system is either the minimum functionality required, or the main happy path. The core can be divided into domain subcomponents, i.e. architectural styles can be combined. Plugins can not only provide functionality, but are a good way to isolate volatile code and reduce cyclomatic complexity. Plugins should have no dependencies between them, and can either be combine or run-time based. While generally the core interacts with plugins through e.g. a function call, they can be communicated with over the network as well. Microkernal can be a hybrid architecture, i.e. you can merge models to build a more powerful approach, like, “get the average of the star ratings”. With this architecture if you have plugins you need some sort of registry to track them, and a well-defined interface.

**Example:** VS Code (most IDEs), Jira, Chrome (most browsers), Insurance (claims processing)

Pros:
- Suitable for applications are installed as a single monolith
- Suitable for problems that require different configurations for each location or client

Cons:
- Distributed as a monolith, it has the same limitations of monoliths: low fault tolerance, low scalability, low elasticity
