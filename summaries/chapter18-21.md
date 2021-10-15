# Chapter 18-21

## Discussion topics
- Architecture decision criteria, e.g. where does data need to live, sync vs. async, auction example (ch 18) - 2
- Documenting architecture decisions with "ADRs", sections: title, context etc. vs. PR templates (ch 19) - 2
- UML, C4, ArchiMate - 2
- Risk matrix to evaluate risks in software (ch 20) - 1

## Diagramming Standards Overview UML
### What is UML?
“Unified modelling language”. A modelling language used to visualize software system design. It “is appropriate for modelling systems ranging from enterprise information systems to distributed Web-based applications and even to hard real time embedded systems”.

Developed by Grady Booch, Ivar Jacobson and James Rumbaugh starting in 1995, it was approved as an ISO standard in 2005. UML has its roots in OOP and, frankly, waterfall development. It was based on the idea that system architecture can’t be demonstrated in a single view, but rather by multiple with different purposes, i.e. 4+1, logical, development, process, physical and scenarios thereof. UML had the goal of being a unified language for representing those different views, a “standard for the artifacts of development”. You get a standardized set of 150 concepts/visual notations, which is criticized for being very complicated. A basic knowledge of how to read and write UML can still be useful, but “most of the UML diagram types have fallen into disuse”.

### How are UML diagrams read?
There are many, many conventions that need to be understand to read a UML diagram. Boxes mean classes, ellipses mean actions, rounded boxes means states, dashed arrows are dependencies, whole line arrows are interactions, etc. To read and create a UML have a “cheat sheet” handy!

### How can I create UML diagrams?
Many drawing tools support UML markup, e.g. Lucidcharts, umlet. There are VS Code extensions you can also use to visualize UML syntax in VS Code (caveat, I haven’t been able to get it to work on my machine). PlantUML: create UML diagrams with text.

### References
- “Unified Modeling Language”, https://en.wikipedia.org/wiki/Unified_Modeling_Language
- “The Unified Modeling Language, Part I“, https://www.youtube.com/watch?v=F5UJkENKc50
- Unified Modelling Language User Guide, 2nd ed., https://learning-oreilly-com.ezproxy.torontopubliclibrary.ca/library/view/unified-modeling-language/0321267974/ch02.html
- UML “cheat sheet”, https://docs.microsoft.com/en-us/previous-versions/visualstudio/visual-studio-2015/modeling/uml-class-diagrams-reference?view=vs-2015
- Online UML diagram tool, https://www.lucidchart.com/pages/landing/uml-diagram-software
- Overview of online UML drawing tools, https://modeling-languages.com/web-based-modeling-tools-uml-er-bpmn/
- Example diagrams, https://lucid.app/documents#/dashboard
- “Drawing a UML Diagram in the VS Code“ https://towardsdatascience.com/drawing-a-uml-diagram-in-the-vs-code-53c2e67deffe

## C4
### What is C4?
“You shouldn’t have to explain what the diagram means, it should stand on its own”. A way of diagramming architecture for people who “don’t know UML”, but still need to communicate what they’re building. Created by Simon Brown in ~2010. The four C’s stand for context, containers, components, code: there are four diagram “zoom levels” that map:
- System context diagram: what you are building and the things around it (what it talks to)
- Containers: the level of architecture diagrams commonly used in the book, i.e. show the overall architecture style. The arrows/links between containers mostly imply communication over a network.
- Components: the major functionality components of the container. Concepts in component diagram should general map to the concepts in the codebase.
- Code: Generally not necessary, unless your component is very complicated.

### How are C4 diagrams read?
The diagrams have no hard or fast rules, they should only “tell the story you want to tell”. C4 diagrams are just boxes of text (name, description, and maybe tech) and arrows between them. Instead of relying on visual notation conventions, brief text is used to explain what is happening. Lines should generally be unidirectional, indication dependency or data flow, with text non the arrow summarizing intent. Shape, colours and size, should enhance a diagram that already makes sense as black and white boxes. Finally, C4 diagrams should use keys rather than a common understanding of notation and be consistent within themselves.

### How can I create C4 diagrams?
Structurizr.

### References
- “Visualizing software architecture with the C4 model”, https://c4model.com/

## ArchiMate
### What is ArchiMate?
“ArchiMate is an enterprise architecture modelling language” developed in The Netherlands 🎉. It’s suited for connecting various areas of a business with it’s technical constituents, like IT and its infrastructure. Or when “you need to show how applications or infrastructure supports business processes“.

### How are ArchiMate diagrams read?
ArchiMate is restricted “to the concepts that sufficient for 80% of practical cases”, to be easy to learn. It is like a subset of UML, having 50 vs. 150 notations/concepts in UML. 

### How can I create ArchiMate diagrams?
- https://www.archimatetool.com/

### References
- “ArchiMate vs Other Notations - 1# - Why you might need ArchiMate?“, https://architecture-center.com/us/blog/109-archimate-vs-other-notations-1-why-you-might-need-archimate.html

There are more… ERD, BPMN, TOGAF
