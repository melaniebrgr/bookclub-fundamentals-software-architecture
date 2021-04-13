# Chapter 6, 7

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

### How are architecture fitness functions incorporated into regular functioning of a project?
I would imagine that FFs would trigger alarms, sending email warnings, or preventing deployments instead of having a dashboard for instance. Some FFs are too important and should be part of a build pipeline, others, like time between bug fixes, you somehow you need a to raise awareness. In a regularly meeting guild of CoP, you could make a point of sharing the metric.
