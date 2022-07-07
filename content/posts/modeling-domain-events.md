---
title: Modeling Domain Events
date: 2022-03-05
slug: modeling-domain-events
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

Domain Event is a powerful modeling tool. From a technical perspective domain event is implemented as a simple immutable data transfer object, but conceptually, domain event is much, much more than that.

## Naming Domain Events

> There are only two hard things in Computer Science: cache invalidation and naming things.
> — Phil Karlton

Naming domain events is no different, but if we understand the nature of a domain event, combined with a few useful guidelines, it is more than manageable.

The defining characteristic of a domain event in the absence of which it has little to no value is that it should reflect an important domain concept. It should tell us that something important happened in our domain. An immutable fact from the past. Even though the name itself implies this, it is amazing how often this eludes us and we end up with some very weirdly named events which convey little meaning and don’t quite reflect the fact that they are supposed to model. For example:

- UserCreated
- ProductUpdated
- ProductStatusChanged

Let’s take **UserCreated** as an example. From a domain perspective, if you really take your time and think about it, can a user ever actually be **created**? What does that even mean? How was the user created? Why? What caused this to happen? Is that what really happened?

More often than not, this is a design smell and **InsertYourNounHereCreated** rarely reflects a domain concept and does not tell us much about what happened. Domain event should mean something and be as explicit as possible (but not too explicit). So, let’s consider these names instead:

- UserRegistered — better, but can it be more granular? In a lot of cases (not all), the answer is yes.
- UserRegisteredByEmail — even better
- UserRegisteredViaGoogle — same here

What about for example **ProductUpdated**?

This one is even worse than UserCreated. UserCreated was at least specific to a point that we could deduct to a certain degree of certainty that a new user entity spurred into existence and that it was somehow created in our system. On the other hand, ProductUpdated only says that a product is now somehow different than it was before, nothing more. To what extent? Why? What does this imply about the state of the product? We can’t really know.

It’s more likely that one of these things might have happened:

- ProductDiscontinued
- ProductPriceChanged (or even ProductPriceIncreased but this is the case where we can get too granular introducing additional accidental complexity without gaining little to no value)
- ProductWentOutOfStock

If UserCreated and ProductUpdated reminded you of CRUD, you were right. Moving away from CRUD requires a “change of mindset”, not just introducing new modeling tools and focusing on what the system does instead on what the system is.

Be as explicit and fine-grained as possible. You can get away with being less explicit and more coarse-grained if not using Event Sourcing for example — but if you are, you have no excuse and you probably missed the whole point of event sourcing if your domain events convey no meaning.

Name them by the outcome that was intended (happy path) or by the reason the use case couldn’t have been executed (sad path).

## What information should our Domain Events contain?

Event name should imply meaning without the need to look into its contents (eg. ItemActivated). Reaching for its contents should only provide us with the actual details that describe the fact that we want to model.

In the case of **SensorActivated** event, there is no need to include properties such as **newStatusName**, **oldStatus**, **newStatus** or **status** — this is implicit due to the explicit naming convention of our event.

Don’t put the same data in different forms eg. an Enum underlying value and ToString variant, only use serialized values, descriptions can be found elsewhere eg. in schema descriptions…

Use primitive types and make your value objects able to serialize or deserialize to/from those types (encode / decode) by different systems other than your own (you don’t know who the consumer might be).

## Final words

Domain events, when read in sequence (eg from our event store, outbox queue, etc…) should tell a narrative about a certain use case/workflow that occurred in the domain that we are trying to model.

For example: “When executing a Place Order use case, given the current state of the Order Aggregate, the command succeeded and the Order was placed, followed by it being Canceled…” which is hard to accomplish with CRUD-like events.
