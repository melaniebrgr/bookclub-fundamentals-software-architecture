# Chapter 4 & 5, "Part3":
 
# Summary
Identifying the driving architectural characteristics is one of the first steps in creating an architecture. These chapters are about defining what an architectural characteristic is, some examples, and how to extract these “-ilities” from the domain concerns, explicit and implicit, and requirements. A key architect responsibility is defining, discovering, and otherwise analyzing all the things the software must do that isn’t directly related to the domain functionality: architectural characteristics. An architecture characteristic is not a functional requirement. It specifies operational and design criteria for success concerning how to implement the requirements. It is a concern critical to the success of the architecture and therefore the system as a whole.

It must meet three criteria:
- Specifies a non-domain consideration: requirements specify what the software should do for the domain, architecture characteristics is how they will be critically supported/enabled
- Influences structure: all systems must have a baseline support for most characteristics, however if it requires architecting something special, then it is elevated to the level os “architecture characteristic”
- Critical to application success: You can’t and don’t even want to support many characteristics, therefore it is important to pick only a few characteristics that are critical to success.

The reason to limit the number of architectural characteristics is because they require design and often structural support and because characteristics are often times in conflict, it can lead to additional design complexity. For this reason you want architecture to be as iterative as possible, so you can change characteristics over time as you learn more.

Architects must uncover the explicit (in requirements docs) and implicit (not in requirements docs) architectural characteristics.

Architectural characteristics can be grouped into three buckets:
- operational: often interact with devops concerns
- structural: shape responsibility for code quality
- Cross-cutting: everything else

## Guidelines for defining architecture characteristics
### Extracting from domain concerns
Listen and collaborate with key domain stakeholders. Keep in mind that you will often be speaking different languages and may need to translate the domain language concern to an architecture characteristic, e.g. time to market -> agility, testability, deployability

### Extracting from requirements documents
Numbers of users and scale commonly appears in requirements documents and often form explicit characteristics; make sure to go over all explicit requirements.

### Extracting from inherent domain knowledge
Having domain knowledge is a benefit because you may realize characteristics you might not otherwise

## Process
1. Listen and collaborate with stakeholders to discuss requirements
2. Review requirements and extract explicit and implicit domain characteristics
3. Remove least important ones until there is a list of no more than 7

# Part3
Two of the three cofounders were invited to discuss the architecture characteristics underlying their application architecture. Here's what they had to say:

## Description
> The overall domain problem the system is trying to solve

Phase 1 of a project is design, estimates, and quoting. There's learning along the way, all these things need to be documented and traced in a particular way. It's a collaborative environment with many different people coming together.

## Users
> The expected number and/or types of users of the system

- Consultant teams can vary widely, 20+ typically, smaller 10-5
- As a company there is a lot of variability 10 - 100
- Competitors have a cost per seat
- They differentiate by not having a limit
- The primary client is architecture firm
- Part of growth strategy is network effect, client is arch. firm, they invite other companies
- Adoption is unpredictable
- No one is working on the weekend

## Requirements
> Domain/domain-level requirements, as an architect might expect from domain users/domain experts

- When a project ends they need to archive it
- It may need to resurface project years later, e.g. for legal reasons.
- Want these 10-100s GB documents into cheaper storage.
- They have regulatory requirements in terms of documentation, and there's different contract types they adhere to, and certain elements need to be listed
Ensuring proper hand off.
- There needs to be an audit log, so everything is traceable

## Additional context
> Many of the considerations an architect must make aren’t explicitly expressed in requirements but rather by implicit knowledge of the problem domain

- Firms are Resistant to change, which so much attention has gone into the the UI.
- Needs to be clear
- Use may be onsite where there is no or low connectivity and needs to work offlines
- Expect users to use modern tools no IE11
- Most don't use Mac, they user MS surfaces

# Architecture characteristics identified:
- usability/achievability
- archivability
- robustness
- localization
- reliability/safety (can't lose documents)





