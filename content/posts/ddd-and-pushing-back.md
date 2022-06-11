---
title: Domain Driven Design and the art of Pushing Back 
date: 2019-06-11
slug: domain-driven-design-and-the-art-of-pushing-back 
tags: ["ddd"]
cover:
    image: "posts/trump-pushing-back.png"
---
When talking about Domain Driven Design, the thing we hear most often is that it’s about the software being guided by the domain, which is true, but I argue that it’s just one side of the coin and cannot stand alone.

The other less emphasized aspect of it is the one where you actually try to understand the problem that the domain is trying to solve, it’s where you push back, challenge the status quo, try to understand the domain/problem itself and model towards first principles.

Id like to share a thought by Michael Jackson (no, not that one) with you, and I urge you to step back and think about it for a second:

> To deal with a significant problem, you have to analyze and structure it…

You might be thinking, well that’s what we do. We take a problem, analyze it, come up with an appropriate model, structure it and then implement it…

Well… Yes, but not really…

What Michael is talking about is that we should analyze and structure **the problem itself first!** — not the system that will solve it (this comes later).

I argue that just blindly following the domain rules presented to us by the domain experts (domain experts are usually not the experts anyway) will not yield the DDD benefits that we strive for, and most often than not, it will not result in a useful and optimal domain model.

In my previous post, I mentioned that users tend to think in terms of their legacy systems and this alone should be enough of a reason not to take everything domain experts tell us for granted.

But, what if there is no legacy system, you say? We are building a greenfield project and our customer only uses paper-based workflows and there is a lot of bureaucracy.

**Paper-based workflows and bureaucracy**

What does that sound like? It sounds like a system to me.

You heard it right, paper and bureaucracy are legacy systems, and should be viewed as such.

*Why is this a problem?*

Well, just transferring concepts from another system (eg. paper-based to computer-based) might not produce optimal results because the concepts that worked in one system may not work so well in a different system. There may not be a mismatch, the concepts may map one to one between those systems but there might be differences or even redundancy.

This is where we should embrace the opportunity (especially if it’s a greenfield project) and try to remodel the process, at least in a tech way. This is where we should engage with the domain experts and try to really understand the problem the domain is solving, structure it and maybe come up with an alternative system which will solve the problem in a more optimal way.

Too many times we agree to small optimizations here and there because we don’t want or can’t push back enough. But still, we need to remember that a number of local optimizations rarely yields a global one and often, a more involved approach needs to be employed.

But don’t get me wrong, this still does not mean that you can pollute the domain with technical terms and implementation details from your code base. Source code is a means to an end and should just help you gain insight and identify emerging patterns and chances for improvement or automation.

## Closing thoughts
In order to successfully practice domain driven design, developers can't just be given requirements. They need to be actively involved in refining business processes and suggest changes to them. Period.

Don’t put them behind the walls of requirements, proxies, and corporate bureaucracy. Domain Driven Design is a powerful weapon and if you “handed it over” to your developers, you have to trust them to wield it.

With that being said, if your developers are not pushing back, something is going terribly wrong.

