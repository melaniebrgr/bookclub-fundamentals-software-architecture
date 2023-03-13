# Chapter 4 & 5
 
# Summary
Identifying the driving architectural characteristics, such as reliability, scalability, maintainability, accessibility, usability, elasticity, etc. etc. is one of the first steps in creating an architecture. Chapters 4 & 5 of the book are about defining what an architectural characteristic is, examples, and how to extract these characteristics or “-ilities” from explicit and implicit domain concerns and requirements. A key architect responsibility is defining, discovering, and otherwise analyzing all of the things the software must do that isn’t directly related to the domain functionality. An architecture characteristic is not a functional requirement. It provides operational and design criteria for success on how to implement the application requirements.

To be an "architecture characteristic" it must meet three criteria:
- Specifies a _non-domain_ consideration: Requirements specify what the software should do for the domain, e.g. "users should be able to place an order and see the delivery time", while architecture characteristics specify how they will be critically supported/enabled, e.g. "system needs **elasticity** to handle bursts of orders around meal times".
- Influences structural design: All systems must have a baseline support for most architecture characteristics, however if it requires building something special, then it is an “architecture characteristic”.
- Critical to application success: Supporting many charactersitics adds complexity so you want to identify the fewest number (3-5) that are critical to success.

Note that characteristics change over time, not only as you learn more about the needs of the system, but because the proirities of an application change as it matures. For instance, for a new application you might prioritise changeability while you are still trying to find "product-market fit" and deprioritise scalability. The reverse is true for a mature product however.

Architectural characteristics can be roughly grouped into three buckets:
- operational: often interact with devops concerns, e.g. availability, continuity, performance, reliability
- structural: help define the level of investment in modularity and code quality, e.g. extensibility, changeability, upgradeability, localizability
- Cross-cutting: everything else, e.g. archivability, legal, privacy, security

## How to define architecture characteristics? Some advice:
1. Listen and collaborate with stakeholders to discuss requirements
2. Review requirements and extract explicit and implicit domain characteristics
3. Remove least important ones until there is a list of no more than 7

### Extract from domain concerns
Listen and collaborate with key domain stakeholders. Keep in mind that you will often be speaking different languages and may need to translate the domain language concern to an architecture characteristic, e.g. if they say, "time to market", you hear "agility, testability, deployability".

### Extract from requirements documents
For example, the numbers of users and scale frequently appear in requirements documents and can be used to inform the characteristics.

### Extract from inherent domain knowledge
If you have domain knowledge yourself you may realize characteristics you might not otherwise.

---

## Example: Part3
Two of the three cofounders were invited to discuss the architecture characteristics underlying their application architecture. Here's what they had to say:

**Description: The overall domain problem the system is trying to solve**

Part3 supports the initial phase of a project, which is design, estimates, and quoting. There's a lot of learning along the way and all these things need to be documented and traced in a particular way. It's a collaborative environment with many different people coming together.

**Users: The expected number and/or types of users of the system**

- Consultant teams can vary widely, 20+ is typical, some smaller 10 - 5
- Competitors have a cost per seat, Part3 does not having a seat limit
- The primary client is an architecture firm
- Part of their growth strategy is network effects, client is architecture firm, they invite other companies to join
- Adoption is unpredictable
- No one works on the weekend

**Requirements: Domain/domain-level requirements**

- When a project ends they need to archive it.
- It may need to be resurfaced years later, e.g. for legal reasons.
- Need to store 10-100s GB of documents a long time cheaply.
- They have regulatory requirements in terms of documentation, and there's different contract types they adhere to, and certain elements need to be listed i order to ensure proper hand off.
- There needs to be an audit log, so everything is traceable.

**Additional context: Many of the considerations an architect must make aren’t explicitly expressed in requirements but rather by implicit knowledge of the problem domain**

- Firms are resistant to change, so the UI needs to be highly useable and clear
- The app may be used onsite (in the field) where there is no or low connectivity. It needs to work offline.
- We can expect users to use modern tools, i.e. no IE11
- Most don't use Mac, but mostly MS surfaces

# Architecture characteristics identified:
- usability/achievability (firms resist change)
- archivability (need to store documents a long time)
- robustness (handle internet connection changes)
- reliability/safety (can't lose documents)
