# Chapter 3

## Component vs. module
Distincitions is not clear and they are kind of equal. Module is more logical perhaps? Component is more physical,
The will create a poll and decide for ourselves: Component, Module, Comodule.

## Cohesion
In code there are several code paths (options for execution). When there are many options (is, switches) from start to end, there is low cohesion. 
If module is making many calls to the same module maybe it belongs together.
If module A is always calling module B maybe they belong together.
How you structure your code to make the best of it, to keep functionality together.
This becomes more important in distructed architectures.

## Coupling
See coupling on the FE as the interpendencies between components, e.g. component file imports other components and composes them.

## Connascence 
Modules dependent on each other but not directly.
A term more used in static type languages, e.g. in GO has name different types of numbers, if you use one number type everywhere you have connascence of type. Another example, in OO langauges that don't support chaining, you cannot call the send before sending the email, which is a problem if that is a required field. Another example, props drilling where you need to pass the same prop multiple levels.

## Modular Unit of JavaScript
There's many different meanings: logical, physical, npm module

In one project started building a new feature: is has a scene, the scene has a graph, the graph opens a modal. The modal is very specific to the scene is it part of the module or a different module. Asked the question: if we remove the modal from the scene does it break the scene? It will not be fully functional but does not "break" the scene. The interaction between the two is the scene emits a message and the modal is displayed. To be fully separate module you would need to ensure the the module API is not "connascent" with the scene.

## What is stable and unstable
Something is unstable if it has mostly outgoing, efferent connections. It is coupled to many dependencies, and if any of those change it is at risk of breaking itself. Something is stable if it has few to no outgoing dependencies, only incoming ones. If it is depended on by many things it is hard to change—and likely won’t be. 

If we have many components depending on the same modal, the modal logic could get complex is it needs to support the 10 cases, might be better to support. As complexity increases we could create a more decoupled situation: event bus the receives the message to display the modal the the modal picks from.
