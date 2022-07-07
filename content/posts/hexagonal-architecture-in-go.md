---
title: Hexagonal Architecture in Go
date: 2022-05-29
slug: hexagonal-architecture-in-go
tags: ["go", "golang", "ports and adapters", "pragmatism"]
cover:
  image: "posts/hexbees.jpeg"
---

> Hexagonal / Ports and Adapters architecture in insert your language here

How many of these have you seen before? Probably too many, but I promise, this will be a short one…

## Why another article?

First, I have a confession to make. I have had this article in my backlog for at least four years now but have never “gotten around” to finishing it due to numerous reasons (the biggest one me simply being lazy). The second biggest reason was “I want to get it right and set the record straight”, but during all this time waiting and planning I have actually fallen into my own trap and would probably just be making more of the same…

## Disclaimer

I do have my preferred way of organizing Go Applications with DDD etc… which is in a constant state of flux (as it should be) and looks 20% different from project to project. I am planning on making a series about those in the future but that is again “just language-specific implementation detail”, what I want to do here is take a step back and approach the subject from the first principles.

Also, I am not trying to downplay or talk badly about the articles out there. I personally have read a lot of them and have helped me immensely, but I do think there is a trap that inexperienced developers in particular might fall into.

## The problem with many articles

The biggest problem I have with a lot of articles out there, and especially due to the fact that we are talking about Go and not some other mainstream language is that most of them boil down to folder structure, which misses the point by light-years. As disclaimed before, the folder structure is important and some are better than the others (I certainly love mine), I will responsibly claim that:

> **Folder structure has nothing to do with Hexagonal Architecture or DDD**

Even bolder claim

> If I see the **ports** folder or **adapters** folder in 99% of the cases I would consider it a code smell **but** it still doesn’t matter, it’s a whole different topic…

If this resonates with you, stop reading right here, but I know for a fact that many people (mostly newcomers or juniors) don’t really think this way and most of the time think folder-structure-first which, unfortunately, gets reinforced with a lot of articles out there in the wild.

## The heart/essence of it

I'm going to start on the other end of the extreme and make another potentially unpopular/bold claim which takes my previous one a level further:

> You don’t need to have a single folder in you application and your application can still be written in a Ports and Adapters style (folders are for code organisation among other things)

If you are really into architecture and into Hexagonal Architecture particularly and you find this as a bold claim, as an exercise I would suggest you stop reading right here, think about the claim I made and go on and try to write your own small proof of concept, preferably refactoring an existing project you have, and while refactoring only think Hexagonal Architecture, don’t think about design patterns, separating infra and business layer, etc…

Ok, enough with the BS, show me the code!

Before showing you the code with no folders in it, I need to make an additional small disclaimer (but a really important one) which I beg you to have in mind while looking at the example:

> File names also have nothing to do with Ports and Adapters (or any style for that matter) — or files for that matter, you can have only a single file.

These depend on soo many things such as your preferred language, and in many cases your chosen code/naming style.

The file naming structure you are about to see is provisional and only one way of organizing this particular codebase. The example is a simple web backend but note that Hexagonal style is universal and will fit any type of application you can think of.

You can find the repo [here](https://github.com/aneshas/whishlist).

There it is, I promise all of the elements of Hexagonal Architecture are there.
The bottom line is: **Know your hexagon**, protect it from the outside world via indirection and thin abstractions and everything else is just a topping — it doesn’t have to sit in a folder, a project, a library, or a module in order to be protected.

If you want to get into more details as to why this still is Ports and Adapters and to know more about a common misconception that people have when employing the Ports and Adapters style (especially with DDD) for which I have also been guilty, stay tuned for my next article talking exactly about those topics.

Cheers and have fun 🥰
