# Chapter 6, 7

## How can we measure architecture characteristics (ACs)
A challenge with ACs is that meanings can be vague and even within an organization there can be differences in opinion in how they’re understood.
- Operational measures: Are easy to measure but there are many different things that could be measured. For example, for performance slightly different performance characteristic can be stressed, e.g. average response time vs. maximum response time, or a performance budget could be created that includes byte download size. Performance metrics can be monitored over time.
- Structural measures: Are harder to measure since there aren’t a lot of things that could be measured that would give a reliable picture of the AC, e.g. cyclomatic complexity is one possibility. Some metrics may not be suitable depending on the language, e.g. distance from the main sequence.
- Process metrics: Some ACs are more measurable when decomposed into their constituents if you can recognize them, e.g. agility can be decomposed into testability and deployability. Metrics for those are more easily determined.

## How to make sure important architecture characteristics are adhered to?
Today we have many more automation tools at hand, and many aspects of architecture governance can be automated. For example, fitness functions (FFs) are a technique that can be used to build “evolutionary architectures”. The FFs are an objective measurement of a characteristic: manual tests, automated, metrics, etc.

Architecture fitness function: “Any mechanism that provides an objective integrity assessment of some architecture characteristic or combination of architecture characteristics”

## Q&A with Jason Santos
### What is a fitness function (FF)?
The FF concept comes from math. Generally the idea is to evaluates large number of variables and reduce it the a single variable, for instance, reduce a number of metrics to a measure of health index. The goal in doing this is so that you will know if measured number goes beyond a certain a point, if it is good or bad. For example, you might not have a single metric for maintainability, but might have several metrics to combine to indicate maintainability. The important thing is that they’re objective. There doesn't have to be more than one variable to be a FF, like a bug fix cycle time could be a fitness function. Some numbers may be more important individually.

### What is the difference between fitness functions and monitoring?
The fitness function bakes in the desirableness value. The FF doesn’t just tell you what you’re uptime is, but includes the threshold for what is good and bad.

### Could a fitness function be unit test coverage threshold? 
That can be called a fitness function. Nothing detracts that from that being a fitness function. If coming to FFs from an enterprise architecture perspective, it is important that the people who need to, have visibility on the value of the FF.

### Are there general guidelines or advice for selecting fitness functions?
The same way you decide you test coverage for instance is how you define the goal of your FF.

### What's the reason fitness functions are not used more on projects today?
The mathethimatical concept is not new, but the use on architecture is new and not widespread. It's only popular among architects who read that book on Evolutionary Architecture for instance. It also has to do with how we are building architectures differently. There is a dichotomy between upfront and iterative architecture. Iterative architecture is new because it is, or was, hard. With cloud architecture, everything has changed, and evolutionary architectures are enabled. Demand has skyrocketed since we’re doing something every week.

### How are architecture fitness functions incorporated into the regular functioning of a project?
I would imagine that FFs would trigger alarms, sending email warnings, or preventing deployments instead of having a dashboard for instance. Some FFs are too important and should be part of a build pipeline, others, like time between bug fixes, you somehow you need a to raise awareness. In a regularly meeting guild of CoP, you could make a point of sharing the metric.

## Architectural Quanta
Definition: an independently deployable artifact with high functional cohesion and synchronous connascence. Independent deployability means that if the component needs a database to function it is included in the deployment. Cohesion here means in the “quantum” the code is unified to a purpose and typical matches a single workflow. Synchronous connasence means that the operational architecture of the quantum is aligned, they are working in concert.

Advantages: defining architectural characteristics at the quantum level rather than the system level will help to identify challenges earlier on. It allows more granular assessment and planning. Analysis might provoke a hybrid architecture, for instance.

