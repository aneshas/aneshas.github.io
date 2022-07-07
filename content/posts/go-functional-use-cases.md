---
title: Go Functional Use Cases
date: 2022-07-07
slug: go-functional-use-cases
tags: ["go", "golang", "ports and adapters", "pragmatism"]
---

I like functions, especially higher-order ones and I think we often underestimate their power when working with Go.

More often than not, we jump to creating a type and attaching a method to it when maybe a simple regular or higher-order function would do (standard library surely, makes use of this eg. http.HandlerFunc).

I employ this approach often and I figured it wouldn’t hurt to share it.

## Where does this come from?

It's everywhere actually (if you squint hard enough). I have dabbled with quite a few languages both professionally and out of curiosity, including functional ones, and have seen the approach implemented in one way or the other both in OOP and functional languages.

People coming from .NET would, maybe call it a **command handler** pattern for example…

## Why?

It all boils down to use cases and how we choose to represent them. In many cases, we will group them by their common dependencies, by an entity they operate on, some provisional grouping, etc… They end up being methods on some **SomeService** type.

While this may work and works most of the time it can lead to some code rot and those use cases being bundled together as they start to share a little bit too much (just because it’s convenient). Another thing that often happens is that files containing those use cases tend to grow larger and larger…

When it makes sense (it often does) I like to model my use cases explicitly and isolate them from everything else as much as I can. I want to have a single place where a use case lives, where its dependencies are listed (eg. adhering to the interface segregation principle), where its parameters and return types are defined etc …

As an example, imagine we are modeling an imaginary use case that will enable clients to open a bank account. You can find the example [here](https://github.com/aneshas/myapp). Take your time to explore it and try to understand what’s going on. It should be pretty obvious.

## Important things to notice

As you have seen there are a few things going on, but the actual thing that I am trying to convey is the definition of the use case as a function and creating another function that acts as a constructor for the use case function and receives its dependencies (provision_account.go file). The constructed use case function closes over the dependencies passed in as arguments to the constructing function so there is no need to store them anywhere (eg. in a struct).

These use cases, defined as functions can easily be taken as dependencies by other objects, such as HTTP servers and interface segregation is also enforced and encouraged there as well. For example, imagine a certain set of use cases being driven by an HTTP JSON adapter and a few others being driven by an event handler adapter, now, those adapters can depend only on a set of use cases they want to drive instead of some object that has a static set of use case methods that we as a consumer can’t control.

This is nothing new and you have probably seen it before (eg. option pattern or when dealing with HTTP middleware, etc…) but I didn’t see anyone using it in this context.

This is of course a simple showcase of this approach and there is more to it, but I will leave that for you to figure out if you decide to try the approach (or send me a message and we can talk about it).

## What might be the benefits of this approach?

Use case separation is enforced and discourages “reuse” between unrelated use case methods.

Enforces interface segregation principle since our use cases now want a very specific set of dependencies (we can still take in a shared dependency such as an SomeRepository, but those should be really thin if you go down that path). As mentioned before, since use cases are scoped this way they are easy to depend on also.

Since the use case itself is just a function it is dead easy to mock and dead easy to test. Just pass the function.

All types (dtos, errors, dependencies, etc…) can be kept in the same file without it getting too big and hard to read and navigate.
