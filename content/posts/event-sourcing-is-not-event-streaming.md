---
title: Event Sourcing is not Event Streaming
date: 2022-05-30
slug: event-sourcing-is-not-event-streaming
tags: ["event sourcing", "ddd", "cqrs", "event modeling", "event storming"]
---

I find it very unfortunate that there are so many negative experiences people have when attempting to implement Event Sourcing most of which turn out to be due to throwing too much infrastructure onto the problem, which as a general case doesn’t work most of the time in any context.

What does this mean?

You do not need an event-streaming platform like Kafka in order to implement Event Sourcing. (That comes later — if at all).

> Event Streaming and Event Sourcing have as much in common as Javascript and Java — **very little to none**

Event Sourcing is really only about **persistence**. You persist a sequence of events/facts which you use to derive the state of your model instead of mutating and persisting the state itself. That’s really all there is to it.

Kafka for example is not built for this, it is a whole different animal and in the context of Event Sourcing, the only place it would be useful is for integrating different domains by publishing integration events to it (note not domain events but integration events, there is a huge difference).

What is a good Event Sourcing storage mechanism then?

Well, unlike platforms like Kafka, you don’t want partitioning, you want total ordering (a flat time-ordered stream of **all** events)

You want the ability to subscribe/read all events in order of occurrence in order to build useful read models, while also having the ability to read a subset of those events related to a single aggregate instance (single id) in order to rehydrate your domain model.

You want to have some mode of opt-in optimistic concurrency checking offered by that storage mechanism.

The list goes on, but these are one of the essential ones.

So what choices do you have then? Here are a few: [Event Store](https://www.eventstore.com/), [NEventStore](http://neventstore.org/), [Go Event Store](https://github.com/go-event-store/eventstore), [an embedded one](https://github.com/aneshas/eventstore), and last but not least roll your own. Rolling your own is really not that hard. I have successfully used SQLServer as an event store and it worked great.

The takeaway:

- Start really small
- Don’t confuse streaming with sourcing
- It’s an append-only log with having certain read guarantees
- Use Event Sourcing specific storage mechanism/library
- Don’t be afraid to roll your own
