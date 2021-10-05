# Chapter 3

## Modularity
The chapter opens by presenting modularity as the central building block of an architect. Modules are how an architect imposes structure on the code.

Question: How would you definition a module in your own words? What is the difference between a module and a component?
Question: What is the “modular units” of Javascript?

Modules are a logical separation, not necessarily a physical one. They can take different shapes in different languages but ultimately they are the way in which that language supports packaging the code together. Modules require a namespace at minumum. The distinction between a component and module is not clear. They are pretty equivalently used. A module is perhaps a more logical separation where a ccomponent is more physical.

## Cohesion
Cohesion is about belonging: how well do the parts of a module belong together. Several flavours of cohesion were defined:
- functional - required for function
- sequential - part of a chain or sequence where the output of one is directly consumed by the other
- communicational - part of a sequence of actions where the output of one is not directly consumed by the other
- procedural - not part of a sequence of actions but must execute in order
- temporal - not part of a sequence of actions but coincidentally execute in order
- logical - operate on the same data type but are not used together
- coincidental - just happen to be in the same source file

In code where there are several code paths (options for execution) or many options, like switches, from start to end, there is low cohesion. If module is making many calls to the same module maybe it belongs together. If module A is always calling module B maybe they belong together. How you structure your code to make the best of it, to keep functionality together? This becomes more important in distributed architectures.

An equation for measuring lack of cohesion is introduced, LCOM. LCOM in general “sums the methods not shared by sharing fields”. A few things to keep in mind 
1. There are many variations of the LCOM equation with output different values for the same input classes, providing slightly different interpretations of cohesion
2. This metric was designed for object-oriented languages and its calculation would need to reinterpreted for other languages.
3. As we just saw there are many types of cohesion, LCOM measures functional cohesion.

One definition of the LCOM from NDepend (1), which is that is simpler to grok and calculate:
LCOM = 1 – (sum(MF)/M*F)
- M is the number of methods in class (both static and instance methods are counted, it includes also constructors, properties getters/setters, events add/remove methods).
- F is the number of instance fields in the class.
- MF is the number of methods of the class accessing a particular instance field.
- Sum(MF) is the sum of MF over all instance fields of the class.

Towards the end of the section, the authors make the point that overall the metric is a calculation of structural cohesion, logical cohesion is not reflected (e.g. string utility functions). We can see an example of that in the LCOM scores above, so we can’t just rely on a score. The chapter provides metrics for measuring if cohesion is going in one direction or another, but cannot state what a “good” value is, and moreover does not offer guiding principles for achieving cohesion, so it leaves it up to the architect to decide. Uncle Bob in his book offers the following however:

> “which parts belong in a module? This is an important decision and requires guidance from good software engineering principles. Unfortunately, over the years this decision has been made in an ad hoc manner based almost entirely on context”. 

Uncle Bob offers three guiding principles:
- Reuse/release equivalence principle (REP): (a “weak” guideline) the parts should “make sense” as a releasable unit
- Common closure principle (CCP): if classes are physically or conceptually bound so that when one is updated so to must the other be, then they below in the same module. (CCP is an expression of the SRP but at a higher level)
- Common reuse principle (CRP): If a module depends on another module but only parts of that module, remove the parts from the used module that the using module does not need.

## Coupling
You see coupling on the front-end as the interpendencies between components, e.g. component file imports other components and composes them. It never is stated outright in the book, but from the discussion of afferent and efferent connections, you get that idea that _that_ is coupling: using or dependency relationships between modules. If parts of a module use other modules to function, then they are coupled. What is the impact of afferent and efferent connections? Again Uncle Bob, for me, gives a better explanation:

- Afferent: Things that depend on the module. A module with a lot in incoming connections requires a great deal of work to reconcile any changes to it with all the requirements and usages of the incoming dependencies. It will be very difficult to change. Because it won’t be changed much it is more “stable”.
- Efferent: Things the module depends on, think: node_modules. A module with a lot of outgoing connections is unstable, it may change if any of its dependencies change.

Afferent and efferent counts are used to measure abstractness and instability.

### Abstractness
The examples of abstractions given are abstract classes and interfaces. The abstractness equation is simply the ratio of abstract type classes to concrete, implementation type classes. A value of 0 means there are no abstractions only implementations, 1 means there are only abstractions no implementations. 

### Instability
The equation (efferent / (afferent + efferent)) is given to measure instability. It implies a slightly nuanced understanding of instability. Something is unstable if it has mostly outgoing, efferent connections. It is coupled to many dependencies, and if any of those change it is at risk of breaking itself. Something is stable if it has few to no outgoing dependencies, only incoming ones. If it is depended on by many things it is hard to change—and likely won’t be.

Restated: Something is unstable if it has mostly outgoing, efferent connections. It is coupled to many dependencies, and if any of those change it is at risk of breaking itself. Something is stable if it has few to no outgoing dependencies, only incoming ones. If it is depended on by many things it is hard to change—and likely won’t be. If we have many components depending on the same modal, the modal logic could get complex as it needs to support the 10 cases. As complexity increases we could create a more decoupled situation: event bus the receives the message to display the modal and the modal component is picked from a list.

### Main sequence distance
The authors showed how by plotting abstractness on one axis and instability on another allows the two metrics can be rolled up into a single metric: distance from the main sequence.

In the "Zone of Pain" modules have a lot of incoming connections, making it hard to change. It is not abstract it is hard to extend. An example of where this is somewhat unavoidable is database schema: database schema are extremely concrete and highly depended on, making updates generally painful. In the Zone of uselessness are mainly abstract components that nothing is depending on. They are usually leftovers that were never implemented. The best position for modules to be on the graph is at highly abstract and stable end (a lot of other modules depend on it) (0,1) and the highly concrete and unstable end (1,0) (it depends on a lot of other modules). See [diagram](https://clevercoder.net/2018/09/08/clean-architecture-summary-review/).

Question: How should distance from the main sequence metric be used? The Distance from the main sequence can be plotted over time to monitor if a module is within an acceptable limit of the main sequence and trigger an investigation when it gets too far.

## Connascence 
Modules dependent on each other but not directly. Connascence is a further refinement of coupling and identification of a number of different types of coupling. “Structured programming only cares about in or out, whereas connascence cares about how things are coupled together. There are static types of connascence that exist only in the source code, and dynamic connascence that only exists at run time. Overall static connascence is “weaker” than dynamic because it is easier to find and change.

Connasence is a term more used in static type languages, e.g. in GO has different types of numbers, if you use one number type everywhere you have connascence of type. Another example, in OO languages that don't support chaining, you cannot call the send before making changes to the response, a connascence of position. Another example, props drilling where you need to pass the same prop multiple levels.

