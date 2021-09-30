# Chapter 1 & 2

Meeting 2: Chapter 1-2

## Architecture
The book opens with its core value proposition: to be a career guide for software architects where there currently is none.
They have four explanations why there hasn’t been one:
- There is no definition for software architecture.
- The scope of the role is large
- The scope of the role is constantly evolving
- A lot of the currently literature on architecture is outdated. Architecture is a product of the environment it was built in.

### 1. Structure
“Structure” or “architectural styles” are the common words used to give an overall picture of how the major components are related, e.g. layered, or microservices. To be able to speak about the structure we all need to share the same dictionary of terms. The structure can depend on the industry, for example, layered is more common in the banking industry. Context is important. If the design system is the product we can consider component design, such as separation between smart and dumb components as an architectural decision.

### 2. Architecture Characteristics
Architecture Characteristics (ACs) are how we define the success criteria of a project. ACs are not clear metrics. For instance, a system needs to be fault tolerant, but fault tolerant by what measure? Architecture characteristics are qualities the architect should use as a compass to guide decision making.

### 3. Architecture Decisions
Decisions are hard rules that constrain an architecture. This was the least clear of the four pillars of architecture for me. One example provided is that the DB layer cannot be directly accessed from the presentation layer, for instance.

### 4. Design Principles
Principles are softer guidelines, not a hard rule like a decision.

Software architecture is the whole of the sum of those four things according to the authors. Martin Fowler in his essay states that “architecture is a social construct, a shared understanding of the design and how the system is divided into components and how the components interact through interfaces. It is the aspects of software considered important by group consensus”.

## Software Architect
A definition is not attempted. Instead, 8 expectations of SAs were shared:
1. Makes architecture decisions
2. Continually analyses the architecture
3. Keeps current on latest trends
4. Ensures compliance with decisions
5. Has diverse exposure and experience
6. Has business domain knowledge
7. Possesses interpersonal skills
8. Understands and navigates politics

Did anything in the list of expectations surprise or stand out?
What do you think will be the most challenging expectation?

To the group, none of the expectaions were necessarily surprising but how much of each is necessary to fulfill the role was uncertain. Also, how do you train for understanding and navigating politics--is this skill just convincing people of things? Some "training" ideas:
- Just experience working clients
- Consider everyone a stakeholder, its never convincing just one person it's a system
- Asking, are there key stakeholders to prioritize?

## Intersections of Software Architecture
This section was a reminder that architecture needs to work with other disciplines, ideally in a synergistic way.
Some intersecting disciples:
- Engineering practice, e.g. micro service architecture is better served by an iterative, continuous integration practise
- DevOps, e.g. scaling / managing microservice requires a strong devops practise
- Process (how teams are formed and managed), e.g. agile practises support more experimentation
- Data, how data is structured impacts how it is consumed by applications

## Laws of Software Architecture
“Everything in software architecture is a trade-off.”
“Why is more important than how.“

There isn't a one architecture style, characterist, or decision suitable for every projects. Each project has different requirements and constraints. Also, the architectural style you're passionate about may not fit your problem.

## Architectural thinking
Architects have a different lens or way of seeing a project according to the authors. There are four ways to see from an architectural eye. They break it into four aspects: seeing design, seeing solutions by having technical breadth, seeing trade-offs, seeing how business concerns integrate with architecture.

## Architecture versus design
To be effective there must be bi-directional information flow between architect and developer so that decisions are communicated and everyone is aligned. A traditional model of architecture vs. design, where the architect establishes the four pillars (style, characteristics, decisions, principles) and component structure in isolation and “throws them over the fence” to the developer to “design”, is ineffective. 

In summary, there is not, or should not be a barrier between architecture and “design” a.k.a. regular development activities, but constant dialog between the two. The architect should be embedded in the teams.

## Technical breadth
An individual’s knowledge can be visualised as triangle with layers: (from bottom to top) stuff you don’t know you don’t know, stuff you know you don’t know, and stuff you know. As a developer, depth, the stuff you know, is more importance for the day-to-day. As an architect, breadth, the stuff you know you don’t know, is more important. Architects must give up some specific technical knowledge.

How do you define breadth? If you can justify the pros and cons for using one solution over another, that is enough to have breadth. If you can implement that's depth.

Question: How can we grow technical breadth an depth? What has worked in the past?

Getting diverse exposure and experience is expected but would take a lot of intentional effort:
- Work on different projects
- highscalability.com (?)
- How to architect it, [video](https://www.youtube.com/watch?v=QOtCpD23118&list=PLhr1KZpdzukdeX8mQ2qO73bg6UKQHYsHb)
- Spend an hour a day or 20 min a day. Bursts of high intensity learning.

## Analyzing Trade-offs
Architectural thinking is about analysing trade-offs. If something is “clear cut” it’s likely the tradeoff simply hasn’t been surfaced yet.

## Balancing Architecture and hands-on coding
Architects should maintain a level of technical depth by continuing to do some hands-on coding. One mistake architects make is being the hands-on owner of a critical software path and being a bottleneck. Framework/critical path work should be done by the team. Some advice for continuing to be involved in day-to-day coding activities:
- Take on some business feature work (this will also mean the architect will feel the pain developers feel)
- Do frequent PoCs, writing the best production code possible when doing so (to be an example, and because it is likely to be incorporated into the codebase)
- Tackle technical debt
- Work on bug fixes
- Work on tooling that automates repetitive tasks carried out by the team
- Do frequent code reviews
