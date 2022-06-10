---
title: A Decade of DDD, CQRS and Event Sourcing 
date: 2019-02-22
slug: a-decade-of-ddd-cqrs-and-event-sourcing 
tags: ["event sourcing", "ddd", "cqrs", "event modeling", "event storming"]
cover:
    image: "posts/ddd.png"
---
> For those that haven’t really moved past the blue book…

DDD for many, including me, brought back the enjoyment of software development. Implementation becomes easy when you break down the domain. The bits and pieces suddenly start to “fit” together in a way they did not before, and the implementation itself becomes straight-forward which results in a simple, maintainable and easy to understand code that will outlive the development team itself.

DDD has come a long way since “the blue book”, but in my experience, not enough people realize that DDD is a growing, evolving thing and that it has indeed learned a few new tricks along the way. This blog is a brief recap of some of the notable things that happened in the DDD community during the last decade or so.

## Can I DDD?
First things first. What do you need exactly to successfully implement DDD? What are the prerequisites without which it wouldn’t be feasible?

According to Eric Evans, there are two main ones:

- Iterative development process
- Access to domain experts

Iterative development is a life force of DDD. It enables experimentation, exploration, and calls for active refactoring of the problem domain as you continue to gain more insight alongside your domain experts. Additionally, you are making use of tight feedback loops which involve feedback obtained through the actual usage of the system that is being constructed.

When you really come to think about it, what are the odds that you have discovered the “best” model for your domain the first time? Even the first couple of times?

The chances are pretty slim. Especially so due to the fact that there is no such thing as “the perfect” model for almost anything that you might be modeling.

One of the significant mistakes we all do is, **slipping towards perfectionism**. As we already made clear, DDD depends on iteration, so don’t get caught up in the details too early. Do the first prototype quickly, then get to the second one quick etc…

**Perfect is the enemy of good** and perfectionism prevents you from doing enough innovation.

With that being said, don’t settle for the first useful model you may encounter. Keep iterating and always rigorously refine and keep watching for even the most innocent looking workarounds. They are an indication of a non-optimal model, and it’s almost certain that you have missed a modeling opportunity somewhere along the way.

Iterative development approach makes heavy use of domain experts. It’s hard to have one without the other, and missing out on any of those will most certainly make your DDD efforts futile.

At this point, you might be thinking: “Well, what about DDD lite?” It provides me with a lot of useful abstractions and modeling tools. Couldn’t I get away by just using the tools and abstractions that DDD lite approach provides?

Sorry, but, the answer is no. DDD Lite can only get you so far due to its nature. It provides a set of modeling tools/building blocks (e.g. entities, repositories, value objects etc…) which will help you implement DDD itself! By only using DDD lite, you actually miss out on DDD altogether…

What use are all of the abstractions and modeling tools, if you don’t have a good idea of what you are building, or even worse… If you are building the wrong thing?

## Explicit context boundaries and the Core Domain
Focusing on the **Core Domain**, as Eric puts it, is a game changer.

Focus your DDD efforts on your Core Domain. The stuff that really makes your company stand out from the competition. The thing that gives you an edge and a competitive advantage on the market.

Companies can waste so much time, money and effort by reinventing the wheel and applying DDD to the parts of their domain that could have gotten away with a more simplistic approach or even be replaced by existing, off the shelf solutions.

But, in order to identify your true core domain, you will need to define **explicit context boundaries** through any of the context mapping techniques (I suggest you look up **Event Storming**, more about it later…).

With all of this being said, it takes a certain level of discipline to keep separation between bounded contexts, but it yields great benefits and almost any project whether it makes use of DDD or not, big or small, can benefit off of context mapping and having explicitly defined context boundaries which will separate really important parts of the domain, from the less important ones, and will ultimately help you identify your Core Domain, and that’s where most of your DDD efforts need to be directed.

## Context mapping and the big ball of mud
What do you do if you are dealing with a legacy system, a big ball of mud? How do you get a taste of DDD there (assuming you still can employ iterative development approach, and have access to domain experts)?

Well, just because the legacy system aka. “the big ball of mud” exists, it does not mean you have to keep cramping it with new features, but rather, employ your context mapping techniques here. Draw a line around it and say, “this is my big ball of mud”, and after that draw a line around your new service and treat it as a separate bounded context.

As Eric puts it, it’s probably inevitable that your service will get enclosed by the big ball of mud eventually (since it will eat almost anything), but at least you had a nice run for a time.

## A word on DDD building blocks
> Building blocks (Entities, Value Objects, Factories, Repositories …) are overemphasized! — Eric Evans

Yes, you heard it right. Building blocks have gotten too much attention, but don’t get me wrong, they are still important and provide a great value. Building blocks are what they are. They are a means to an end, mere implementation details that help you implement strategic DDD patterns.

As Evans stated, he regrets putting the strategic patterns way back at the end of the book, which probably resulted in many people giving more importance to the tactical patterns because they come first or even worse, they get so caught up in the intricate implementation details of tactical patterns, they don’t even get to the most important part of the book.

The thing to take away is that building blocks provide you the tools to implement DDD, but you should give much more focus to strategic patterns, even more so because tactical patterns/building blocks will continue to evolve, some will become obsolete, new ones will be added (eg. Domain Events).

## Aggregates
Aggregate represents a conceptual whole in the domain that is also consisted of other small parts (Value Objects and/or other Entities) and protects an always consistent invariant across all of them.

One question that pops up often is a concern that a lot of people have regarding the awkward cases where their aggregates have an invariant that crosses thousands of entities.

Since we can access a child entity only through its parent aggregate, do we load all of them each time we load an aggregate? Do we make use of lazy loading? Do we model this differently even though it’s a business invariant? If yes, what’s the correct model for this?

The bottom line is that OO is really not good at handling collections of objects, especially very large collections, which calls for loosening and “bending” the rules a bit in these cases.

The same applies if you have a small number of aggregates but have a lot of concurrent users that might be interacting with the aggregate at the same time.

In cases like these, you might consider modeling those entities as separate aggregate(s) and try enforcing the business invariant on a higher level. For example, in domain services, process managers/sagas etc…
In short, make the consistency an explicit concern of your domain instead of it being solved implicitly through the infrastructure.

As it turns out, another potential solution is related to another question/concern that keeps popping up when working on a project that makes use of **CQRS** as a standalone pattern or in a combination with **Event Sourcing**.

**Can write side query the read side?**

According to Greg Young, the answer is
**yes, absolutely, there are cases when you simply have to**, and one of those cases is related to the challenge we mentioned here.

I’d argue that even if you don’t face the aggregates/entities problem we describe here, there are a lot of cases where it’s OK to query the read side (I have certainly done it more than once).

It’s fairly easy to spot these opportunities because in majority (if not all) of the cases they tend to present themselves in a form of a specification pattern, but since you are using Event Sourcing or CQRS as a standalone pattern, you can’t really make use of them.
But luckily for you, specifications and CQRS are two competing/interchangeable patterns.

Rule of thumb would be to aim for very small and very specific projections which can provide you with a very specific answer to a very specific question which would be very cumbersome to implement by querying domain models.

Vaughn Vernon has a lot to say about aggregate design.
Check out his two-part Aggregate Design paper:

- [Effective Aggregate Design Part I](http://dddcommunity.org/wp-content/uploads/files/pdf_articles/Vernon_2011_1.pdf)
- [Effective Aggregate Design Part II](http://dddcommunity.org/wp-content/uploads/files/pdf_articles/Vernon_2011_2.pdf)

I also highly recommend you check out his DDD book: [Implementing Domain-Driven Design](https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577/)

## DDD in a modern “always on” world
Software applications outside of the enterprise world, in general, have quite different requirements in terms of performance, latency, responsiveness, and scalability. There was a fear that applying DDD patterns to these kinds of domains would not really be feasible due to the aforementioned constraints and the overhead that OOP with DDD applied would introduce.

This might have been a great obstacle to widespread DDD adoption, but luckily, applying DDD to these kinds of domains gave birth to a new approach (the ideas were there for centuries actually) towards applying DDD under the name of Event Sourcing and CQRS.

In short, Event Sourcing and it’s complementary pattern, CQRS gave us an extravagant revamp of DDD building blocks, and a way to employ DDD patterns through the use of Domain Events as first-class citizens and the sole source of truth in these kinds of systems, while at the same time allowing us to satisfy high throughput / high availability needs of those kinds of systems, by enabling us to scale reads and writes separately, and employ inter-service integration via Domain Events.

Event Sourcing also provides a stepping stone towards implementing DDD in a functional world, due to the immutable nature of its event streams (An aggregate state is a left fold of all of its events).

But meeting scalability demands of large distributed systems is not the only benefit of employing this kind of event-centric approach towards modeling our systems.

There are a number of other benefits of employing an event-first modeling approach:

- Explicitly modeling important domain events and formalizing them, forces domain experts to think in terms of the behavior of their system instead of in terms of its structure. This especially helps, since people tend to think in terms of their legacy systems, instead of focusing on the problem they are really trying to solve.
- By modeling events, and focusing on the behaviors instead of nouns, even the domain experts get a different perspective on their domain and gain additional insight.
- Event modeling forces temporal focus and makes time become a crucial factor (which it is)

If any of these resonate with you I encourage you to check out [Event Storming](https://www.eventstorming.com/) by Alberto Brandolini. Event Storming employs an event-centric approach in order to distill the domain.

I won’t go into detail here, but I will just mention that Event Storming has a number of different flavors you will find on the site and the [book](https://www.eventstorming.com/book/) but, I would like to mention one more variant by Greg Young.

In his variant, you basically just take one single long-running business process end to end and model it using Event Storming in order to discover your service boundaries. This worked very well for me.

## Event Sourcing and CQRS misconceptions/pain points
During one of his talks, Young focused on some recurring pain points/misconceptions that were coming up repeatedly regarding Event Sourcing and CQRS, and offered clarification and advice on how to approach these …. Here is a short recap.

> CQRS is not a top-level architecture!

CQRS is a supporting pattern and you need to treat it as such. Don’t go crazy! Instead, apply it selectively to a few places.

> Commands must return void?!

The bottom line is that it’s not about return values, it’s rather about side effects? It is perfectly OK for commands to return the list of errors example, instead of relying only on throwing exceptions (which is a bit of a bad practice anyway).

> Command vs Domain Event is not strictly a one on one relationship!

An event does not necessarily have a corresponding command, nor does a command have exactly one corresponding event being published.
It is important to understand that there are always two sets of use cases. The commands coming in and the events coming out.

An event is not strictly a result of a command coming in. In event-centric architectures, this is commonplace to see, and the whole point of it is that events cause stuff to happen. A business process that resulted in publishing a domain event is often time triggered by another event without any commands.

> There is no such thing as one way / async Command

The whole point of a command is that I have the ability to tell you No!

“Async” commands don't really give you that option, you just fire and forget, which is kind of defeating the purpose. They do not work well in the real world.

By accepting a command, it should mean that you validated it, you can execute it, you processed it and it’s done. Otherwise, what you really want is a downstream event processor.

> Don't write a CQRS / Event Sourcing framework. Period.

I think we need to start realizing that you do not need a framework for everything. Frameworks have their place, but we need to put an end to framework-first mindset and instead, try to solve our problems with focused modules/libraries instead of relying on almost always “too generic” frameworks which tend to sprawl their tentacles all over our code base.

> We need better examples!

As Greg puts it, we need better examples. Event Sourcing is hard, that’s a fact, and simple examples like simplified shopping cards don’t really do it justice.

Recommended training material:

- [Domain-Driven Design Distilled](https://www.amazon.com/Domain-Driven-Design-Distilled-Vaughn-Vernon/dp/0134434420)
- [Implementing Domain-Driven Design](https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577/)
- [Event Storming](https://www.eventstorming.com/)
- [Event Storming Book](https://leanpub.com/introducing_eventstorming)
- [Microservices Patterns: With examples in Java](https://www.amazon.com/Microservices-Patterns-examples-Chris-Richardson/dp/1617294543/)
- [Confluent Microservices blog series](https://www.confluent.io/blog/data-dichotomy-rethinking-the-way-we-treat-data-and-services/)
- [Lightbend Courses](https://www.lightbend.com/learn/lightbend-reactive-architecture)
- [How Events Are Reshaping Modern Systems](https://www.infoq.com/presentations/systems-event-driven)

This blog has also been published at [tacta.io](https://tacta.io/en/news/a-decade-of-ddd-cqrs-and-event-sourcing/7)

