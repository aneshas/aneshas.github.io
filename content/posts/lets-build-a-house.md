---
title: Let’s build a house 
date: 2020-02-04
slug: lets-build-a-house 
tags: ["ddd", "sofwtare"]
cover:
    image: "posts/city.jpeg"
---
When talking about software, we often hear the term “architecture” mentioned a lot. That inevitably reminds us of buildings and construction. While this may be true up to some extent, there are a lot of discrepancies between the approaches we take towards architecting a building (a house for example) and a typical web application software system. Much more so if we employ agile practices while doing so (which I hope we all do).

Software architecture is more about defining and formalizing constraints and gathering quality attributes that we need to satisfy while implementing business requirements.

A good architect tries to defer most of the architectural decisions that don’t affect the most important quality attributes directly. These decisions can then be made downstream by the developers in charge of building the actual solution (the architect himself should be one of them).
This indeed means that software architecture “is not” about making “all” of the decisions upfront, but rather, only the important ones.

Let’s look at a simple example. Let us contrast building a house in the real world versus building a virtual house (a hypothetical software system, might be a simple web application).

Some things of concern, but not limited to might be:

1. Land (Infrastructure)
2. Floor plans (Architecture / technical diagrams)
3. Foundations (Initial project setup)
4. Floors and the roof, walls, bulkheads, etc… (Software Layers)
5. Functional rooms + furniture (Actual features that bring value)

So how do these compare?

## Land (Infrastructure)
When building a house we need to purchase (allocate) the entire piece of land that our house will sit on top of. Plus, we need to account for some more if we maybe decide to make some extensions to our hose (a garage maybe, a garden …).

This implies that most of the time we need to know the size of the land needed upfront which in turn implies that we are required to make a large upfront cost in order to purchase the land even before we even start with the actual construction.

In contrast, when building a software system the agile way, we try to avoid these upfront commitments. Why? Because we can!

Why is this the case?

Ask yourself, what is software? If you think hard enough, you will come to the conclusion that software, in essence, is just a pile of text, compiled to machine language (instructions) in order to be executed to (hopefully) perform some useful work for us people.

And what is the nature of “text”.
Well, most importantly, text can be changed, expanded, erased, reorganized, burned and thrown away. It’s subject to change.

If you think otherwise, you are living a lie and becoming aware of this asap will do you much, much good.

But even if you choose not to be aware of this, I can tell you one thing for sure: The clients are!

So, going back to our example, how much land (infrastructure) do we allocate for our software system? The answer is, as little as possible, or to put it differently, only as much as we need to.

Staying agile is all about iterations, tight feedback loops and building as little as needed when we need it.

We try to avoid making big upfront commitments and incurring costs that are uncalled for. As a side note, if you’ve ever wondered what cloud computing is all about, now you know (pay only for what you use)…

For the software system in our example (our virtual house), we would allocate/purchase only enough resources we need for our first iteration, feature or sprint. Nothing more, nothing less, because unlike with land, we can always but more.

## Floor plans
When building a house in the real world, in 99% of the cases we have the whole plan ready upfront. We hire an architect, decide on almost all features (rooms, layout), materials, etc and again, we make another upfront payment and only now we can start building foundations for our house.

After this point, pretty much every decision is immutable, and any change to the initial plan is hard to make or would surely incur a lot of extra unplanned cost because once concrete hardens it’s really tough to break.
That’s just the nature of it.

We take this for granted because we understand the reasoning behind it and have learned to live it.

But surprisingly this isn’t true for software. Many people still compare building software with building houses, and this cannot be further than the truth.

As we said, software is different. A good architect does not make all of the decisions up front. Why? Because software is easy to change (and will change, it’s just text) so we don’t want to limit our legroom that we will most surely need later.

Most importantly, we don’t want to spend any more money than necessary. Will we like that bedroom on the second floor? Will we even need it?!

## Everything else
After we have the foundations are laid down, it’s time to start building our floors.

Floor by floor, layer by layer, weeks and months pass while we wait with our fingers crossed and hope for the best.

Finally, when the house is done, final work can begin and only then can we start throwing in the furniture.

A few months later, we finally get to use our house.

I think you can see the pattern by now.

Architecture deals with horizontal slices. Floor by floor, layer by layer, because it’s easier to do it this way (and it's cost-effective).

But when building software systems, we deal with vertical slices (or should). What does this mean?

When creating software solutions, we start from the most important thing (the core), build all the vertical slices for it, and then work our way out (horizontally) by adding new features to the core or improving the core itself.

In our virtual house example, this could be anything really, but let’s take a bedroom as an example.

Let’s pretend that we sat with the customer and decided that having a place to sleep in asap would be of the highest priority.

Thus, our main goal should be to deliver a single useful feature for our customer which can be tested out and for which we can get constructive feedback at the earliest moment possible.

I hope you can understand why this can be useful (in contrast to waiting for months for first feedback)

So, some of our basic goals are:

- To make as small number of set in stone decisions as possible
- Avoid the unnecessary upfront cost
- Have something ready as soon as possible (Something useful)
- Get feedback from the customer at the earliest possible moment

How would we go about doing this? We do the simplest thing. We simply follow the path of the least resistance. In analogy to the real house, building our virtual house might follow steps similar to these:

- We allocate just enough “land” for a single bed.
- Build just enough of foundation that can accommodate our bed + some walking space around it
- Next, the bed comes in
- We put up a cheap set of walls (non-concrete ones)
- At last, we cover our small bedroom with a makeshift roof, just enough to keep the rain out.
- And… we are done.

We are now ready to call in our client and receive some constructive feedback about it. Hell, he could even spend the night.

Once we have our feedback, the client decides what is the next most important thing for him…

- It might be to thicken the walls and make them production-grade.
- Maybe it will snow soon, and we should put up a more serious roof.
- Perhaps he wants to experiment with the interior decoration of the room.
- Or maybe this is just what he needs, it will be enough to sleep in for some time, and now he would like us to add a toilet adjacent to our bedroom.

This way we ensure that the customer always **gets what he wants, and not what he asked for!** — Remember what we said about the nature of software! Customers have a nose for this and they will always want something other than what they initially specified.

So in a nutshell:

- You start from the core, do as little as possible, but usable.
- Gather feedback, decide on what’s next.
- Rinse and repeat!

## Final words
If you take away anything, let it be this:

Building software is nothing like building a single house/building.

Building software is much more involved than this. To build, evolve and maintain a software system is more similar to city planning than to building a single house. (Let’s face it, it’s never a single house anyway).

Cities like software, have lives of their own. Cities evolve, grow (or even shrink) in size. New buildings are added (features) all the time, old ones are refurbished or demolished(refactoring).

New water and heating lines are added, removed and replaced on a daily basis. Metro lines are bored under the city.

While doing all of this, you can never shut down a city. You can close down some parts of it but as a whole, it must always remain functional.

This is why building software is neither simple nor easy, but only by embracing change, and failure (this might be a topic for another blog post) we can be prepared, and triumph!



