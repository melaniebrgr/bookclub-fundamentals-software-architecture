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

## Connascence 
Modules dependent on each other but not directly.
A term more used in static type languages, e.g. in GO has name different types of numbers, if you use one number type everywhere you have connascence of type. Another example, in OO langauges that don't support chaining, you cannot call the send before sending the email, which is a problem if that is a required field. Another example, props drilling where you need to pass the same prop multiple levels.

## Modular Unit of JavaScript
There's many different meanings: logical, physical, npm module

In one project started building a new feature: is has a scene, the scene has a graph, the graph opens a modal. The modal is very specific to the scene is it part of the module or a different module. Asked the question: if we remove the modal from the scene does it break the scene? It will not be fully functional but does not "break" the scene. The interaction between the two is the scene emits a message and the modal is displayed. To be fully separate module you would need to ensure the the module API is not "connascent" with the scene.

## What is stable and unstable
Something is unstable if it has mostly outgoing, efferent connections. It is coupled to many dependencies, and if any of those change it is at risk of breaking itself. Something is stable if it has few to no outgoing dependencies, only incoming ones. If it is depended on by many things it is hard to change—and likely won’t be. 

If we have many components depending on the same modal, the modal logic could get complex is it needs to support the 10 cases, might be better to support. As complexity increases we could create a more decoupled situation: event bus the receives the message to display the modal the the modal picks from.
