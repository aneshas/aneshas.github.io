---
title: A Case for Event Sourcing
date: 2022-05-30
slug: a-case-for-event-sourcing
tags: ["event sourcing", "ddd", "cqrs", "event modeling", "event storming"]
cover:
  image: "posts/chain.png"
---

You must have heard these before:

> Bad programmers worry about the code. Good programmers worry about data structures and their relationships. — Linus Torvalds

> …Show me your data structures, and I won’t usually need your code; it’ll be obvious. — The Mythical Man-Month

> Smart data structures and dumb code works a lot better than the other way around. — Eric S. Raymond

Of course, when dealing with software, **it always depends** but as a general rule I find these claims to be largely true.

If you look at any piece of software, spanning from a whole range of different databases (most of the time the basic difference between them are underlying data structures they use), moving a level up, data modeling techniques and even further up entity/domain modeling, one thing they all strive to do is to pick the best data structure for the problem at hand depending on a variety of different constraints, eg. storage medium in case of databases, access patterns in the case of data modeling/table normalization and business concepts in the case of enterprise application modeling which we will look into further.

## The Problem

When it comes to modeling our Entities and Aggregates we are faced with the ever-present object-relational impedance mismatch which always leaves us with our object/domain model being coupled in one way or another to our persistence data model (eg. SQL tables).

No matter how hard we try it’s always there. With this being the case, we are forced to know our data structures ahead of time. This would be no issue if the users knew what they wanted, right :)

The domain model is a living thing. It is always in a state of flux and changes as we learn more and more about the problem at hand. More often than not this change is hampered by that link with the underlying persistence model and more often than not, we simply give it up or do it poorly due to the ever-present overhead of keeping the tables up to date, migrations and rollbacks, data consistency concerns, fear of messing up, etc…

## How Event Sourcing Helps

One might argue that with Event Sourcing we have the same setting which is true in a way but still fundamentally different.

With Event Sourcing, we turn the situation on its head. We emphasize what the system does instead of what it is and force our persistence model to conform to our domain by persisting pure domain facts (Domain Events).

This creates only a one-way coupling from our persistence model which is an infrastructural concept to our domain which is totally acceptable. This can also go very wrong if we fail to model our domain events properly (Read more about it in [Modeling Domain Events](/posts/modeling-domain-events)), but for the sake of this article let’s assume we did that part right. To be totally honest, even if we didn’t we can still make use of the following…

Now, with our event log in place, we gain access to a superpower.

That superpower is called **being able to effortlessly evolve and change our data structures as we learn more about our problem domain**.

(If you think that’s a long name, try [Rindfleischetikettierungsueberwachungsaufgabenuebertragungsgesetz](https://www.salon.com/2013/06/03/law_change_spells_end_for_germanys_longest_word_ap/))

With every new insight we get, we are free to create, delete or refactor our entities, value objects, even aggregates, and employ different design patterns and object modeling techniques without a single migration, only by interpreting our stream of events in a different way and re-building our in-memory data structures from immutable facts which stay exactly that, immutable without affecting the integrity of our existing data.

This might seem obvious but I don’t think it’s emphasized enough. We mostly hear how event sourcing helps us **rebuild our state from the event log** — but what does that really mean? I hope now it’s a bit more clear.

The other reason why this is worth mentioning is that it is related to **dealing with change** which is basically all that we do in the software industry.

This ability is priceless on the command/write side, but it doesn’t stop there, we also have the same freedom on the query side (this one is more obvious) where we are able to build our data model based on any possible constraint that might apply in any given context.

I hope this gives you an incentive to try it out for yourself. If it does and you happen to like C# or Go maybe these couple of libraries can be of help (although I would advise going without any libraries at first):

[Tactical DDD](https://github.com/aneshas/tactical-ddd), [Go EventStore](https://github.com/aneshas/eventstore), [Liquid Projections](https://liquidprojections.net/)

Also, feel free to check out some of my other articles about:

- [Modeling Domain Events](/posts/modeling-domain-events)
- [Microservices](/posts/missing-the-point-with-microservices)
- [DDD and Pattern Thinking](/posts/domain-driven-design-and-pattern-thinking)
- [Building Houses](/posts/lets-build-a-house)
- [DDD, CQRS, ES](/posts/a-decade-of-ddd-cqrs-and-event-sourcing)
- [Ports and Adapters](/posts/hexagonal-architecture-in-go)
- [DDD and Domain Experts](/posts/ddd-and-pushing-back)

Thank you for getting this far ❤
