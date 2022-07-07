---
title: A Decade of DDD, CQRS and Event Sourcing
date: 2022-02-20
slug: missing-the-point-with-microservices
tags:
  [
    "event sourcing",
    "ddd",
    "cqrs",
    "event modeling",
    "event storming",
    "microservices",
  ]
---

By now, even the birds on the trees got the memo that microservices are not a catch-all magic pill that will fix all of your organizational and product issues seemingly caused by a monolithic way of thinking.

More often than not organizations fail spectacularly by carrying over this monolithic way of thinking when decomposing their systems towards more decoupled (hopefully) microservices architecture and end up having even more issues and higher incurred costs as compared to the good old monolith.

In what ways can this go wrong?

## Big bang release and delayed delivery of value

While most of us agree that big bang releases rarely work when mentioned in the context of rewriting any decently sized piece of software, this concept somehow seems to elude us when venturing on an endeavor of breaking our monolithic system into microservices and we gladly set ourselves on a path of months or even years of refactoring towards a more complex distributed system without effective feedback nor the chance to reflect on it’s value.

In order to avoid this pitfall (or almost any other when delivering software), as an organization, you must constantly ask yourself:

> Am I delivering value on a regular basis?

If the answer is no then take a step back and rethink your strategy.
Breaking a big system down to an unbounded small set of services does not necessarily imply a large-scale refactor. Rather, continue delivering value and strangle your monolith by continuously identifying areas of the system that might be good candidates for being refactored towards autonomous services.

Grow your microservices just as you have your monolith: **organically while continuously delivering value to customers** (potentially at a smaller rate).

NOTE:
Deploying to test environments and passing QA is of little value to anyone.

## No strategic decomposing strategy

There has to be a method to the madness. Another major thing that a lot of organizations miss is the strategic approach towards decomposing their systems towards autonomous entities. One of the most important (and hardest) things in developing any kind of software system is the “clear definition of boundaries”.

I have seen people starting down on a journey of breaking their systems into microservices without a clear strategy and hoping that correct system boundaries will somehow implicitly present themselves. While it is true that this always happens to a certain extent, and always will due to inherent fuzziness of customers' wants and needs, it does not mean that directed effort towards defining logical business-driven bounded contexts should be avoided.

In order to effectively break your system down, you first need to understand the whole, and when I say the whole, I do not mean your current monolithic system because it has been polluted and probably turned into a big ball of mud (which every system strives to because of entropy…) and does not reflect business and domain boundaries in a realistic way.

When starting on a journey of “The great de-composure”, don’t decompose your current monolith, but rather **“Decompose the domain”**.

I highly advise you to employ an exercise such as Event Storming where you take a step back together with the customers and domain experts and try to understand your problem space from the first principles without the constraints of the monolithic system you already have.

If a full event storming session is for some reason unacceptable I advise doing it for the largest end-to-end use case in your system in order to correctly explore and understand business boundaries.

## Interservice communication and dependencies

What do you get if you break up your monolithic system into 20 services that have hard dependencies on each other due to improper decomposition which inevitably causes implicit business coupling (each use case involving crazy spaghetti communication ripple..) and/or due to improper communication mechanisms employe, eg. hard dependencies to other services, dependencies on data from other services (you might as well share the DB), over-reliance on synchronous modes of communication, making breaking changes to deployed contracts, etc…?

You get the same monolith you had plus potentially 20 additional teams, you have increased your failure surface by orders of magnitude because you have exchanged your safe in-process method calls with calls over a network that is inherently unstable, threw the safety of acid transactions your monolithic database provided… Should I continue?

In short, you exchanged your complex system for a more complex and expensive one with only negligible and marginal benefits.

If your service is not independently deployable, testable, and evolvable — it has failed.

## Size

Except for complexity one of the major reasons we decide to break our monolithic system down, is its size. When decomposing, we must not forget this. Don’t disregard the “micro” in microservices. Make them as small as possible but not smaller. Try thinking in terms of **Microsystems** first and Microservices second. What does this mean? If you really tried but after all of the efforts your service ends up being too large every time even after employing a strategic approach, more often than not it is an indication that you have discovered a natural business boundary, a bounded context in your problem space which you can regard as a **Microsystem** instead of a single potentially monolithic microservice.

Break it down into further services but protect it from other services with a single entry point (think gateway service for your microsystem) which will hide these supporting services internal to your bounded context.

We all have an inherent feeling when something is too big. If your service feels too big, it probably is and if it feels convoluted and wrong, it probably is.

Follow your gut feeling.

## Use case orchestration and ACID

In so many cases people forget that when they break their system down and introduce network calls in place of good old synchronous in-process method calls, “you throw out transactionality”. Saving an entity, then calling another service to initiate some action, and sending an email via another service all at the same time while executing your use case handler will simply not cut it in a distributed system.

What happens if any of those fails? Can you reliably retry without the system it breaking down? Most of the time the answer is a resounding NO.

When you distribute your use cases across multiple services don’t stay in the box of synchronous communication. Start thinking in terms of reactive systems, take the last step towards truly autonomous services by introducing event-based communication and making previously synchronous actions asynchronous. Don’t synchronously send an email, do it out of the process by for eg. having a microservice listening for a certain event and reacting to it. (Remember the SRP?)

Once you are in the world of event-based communication you will have to learn about and employ process managers/sagas, but they are not nearly as complex and as mysterious as people make them be, in fact, they are a necessity.

## No retry mechanisms at service boundaries

The last thing I will mention is the lack of having retry and circuit-breaking mechanisms at the boundaries of your microservices.
Note that this applies even to monoliths when they communicate with third-party services.

The network is inherently unstable. This is a reality, but this doesn’t mean your clients need to know about every hiccup inside your system. Most of those failures are transient and can be recovered from by simple retry mechanisms at points of integration, but for some reason, this seems to elude many people.

## Coupling services via tests

Services are supposed to be independent, decoupled, and autonomous. DON'T COUPLE THEM WITH E2E TESTS. Avoid elaborate setups of n number of microservices in order to test for an edge case. Keep this number of tests to a minimum and run them against a production similar environment (hopefully created on demand). Your service should be able to live in its own world (unless it is a gateway or an aggregator) and be 100% safe to test and deploy **without ever testing its interaction with real instances of other services.**

This is just a short list of many pitfalls of microservice architecture that one might encounter and much more could be said on those alone, but they are some of the most dangerous and most common ones that I thought were worth mentioning.

Remember

> Software engineering is about solving problems by using software! Don’t get caught up in dealing with accidental (technical) complexity instead of the essential one. The code is not the point.

Thanks
