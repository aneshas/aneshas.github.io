---
title: Domain Driven Design and Pattern Thinking
date: 2020-11-27
slug: domain-driven-design-and-pattern-thinking
tags: ["ddd", "patterns"]
---
Design patterns are very useful things in general and they pop up a lot if you are applying DDD in an OOP context (If you’re there you are probably already applying Tactical DDD patterns).

One principle I want to emphasize here because I see so many violations of it, is the following: **Don’t use pattern names when implementing a pattern**.
It’s amazing how people keep missing the point.

Applying this principle is actually very helpful in double checking if you are applying the right pattern to the right thing. What do I mean?
If you are finding it hard not to add that Strategy, Builder, State, Specification postfix or prefix to your pattern implementation, that might be a good sign that you were guided by the patterns-first approach, instead of domain-first and that there is a good chance that you have misunderstood an important domain concept in eagerness to employ a specific design pattern.
(This does not only apply to DDD, it’s a good practice in general)

Pattern names should be invisible in your codebase, and they should be replaced with domain concepts instead.

Patterns provide solutions for **classes** of problems that are applicable in **different contexts**.

**Context is the king**! but still, context is so often disregarded and we jump straight to implementation without understanding in which context we are operating.
The reality is that everything depends on the context.
That is the reason why patterns have those generic names that they have: Singleton, Builder, Factory, State, etc…
The basic premise when using patterns is not to force them. Let them present themselves in your particular context, which will, in turn, reflects to the names also.

A pattern must have meaning inside of your domain. For example:

Instead of XXX**Strategy**, an XXX**Policy** might be more appropriate (or maybe you don’t even need the suffix)

Instead of XXX**State**, use a domain concept such as **ClosedAccount**, **ActiveAccount**, etc…

Pattern thinking heavily influenced Domain Driven Design (and yes Eric put patterns to context and didn’t use “Pattern” in the title — He called it Domain Driven Design)

