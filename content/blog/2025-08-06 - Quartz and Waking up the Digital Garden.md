---
date: 2025-08-06
aliases:
  - Waking up the Digital Garden
tags:
  - digitalgarden
summary: A returf of the digital garden, the reasoning behind it
type: blog
status: published
---
![[img-DG-GlobeObs-Sora.jpg]]
# Waking Up My Digital Garden

Something clicked over the past couple of days that made me want to tackle my sleeping digital garden. It's been a couple of weeks since I cancelled Obsidian Publish, and I've been thinking about what comes next.

The truth is, I had Obsidian Publish for two years but wasn't really using it. Not properly, anyway. It felt like having a beautiful greenhouse that I'd built but never quite got around to planting. The potential was there, the structure was solid, but something was missing - that spark of genuine engagement that turns a collection of notes into something alive and growing.

## The Itch to Tinker


I love the process of learning, and I especially love tinkering. There's something deeply satisfying about taking something apart, understanding how it works, and putting it back together - ideally making it better in the process. Obsidian Publish was convenient, sure, but it was also a black box. Click a button, content appears online. Efficient, but not particularly engaging for someone who enjoys getting their hands dirty with the mechanics of things.

That's when I started thinking about digital gardens as more than just published notes. The best gardens aren't just displays of what's already grown - they're living systems where you can see the gardener's hand at work, the experiments in progress, the seasonal changes and gradual improvements over time.

## The Cook One Thing Philosophy

I've been developing this concept I call "cook one thing", born out of the idea of one recipe a week as a way of learning to cook - the idea that mastery and satisfaction come not from juggling dozens of projects simultaneously, but from giving complete attention to one thing at a time. It's about resisting the modern urge to multitask and instead discovering what emerges when you let one idea develop fully, naturally, without distraction.

This philosophy feels perfectly aligned with tending a digital garden. Rather than trying to publish everything I think about, although the concept of seedlings isn't lost on me, I want to be selective. My main vault contains daily thoughts, weekly reflections, work notes, random observations - the full spectrum of mental activity. But not everything needs to go out to the web. The digital garden should be the distilled essence, the ideas worth cultivating in public.

## The Technical Rabbit Hole

What started as a simple desire to get my garden growing again quickly became a fascinating technical challenge. I discovered Quartz, a tool that transforms Obsidian notes into fast-loading websites with all the features you'd want in a digital garden - backlinks, graph views, search functionality, the works.  As part of that discovery I also found it had won many hearts within the Obsidian community: [GEMS of 2023](https://obsidian.md/blog/2023-goty-winners/)

Setting it up properly requires navigating a maze of tools and services. Git repositories, Node.js dependencies, build processes, deployment pipelines, SSL certificates - the works. For someone who loves tinkering, this wasn't a deterrent; it was an invitation.

I spent the better part of a day or so wrestling with the setup, making mistakes, starting over, learning the hard way that not all advice translates perfectly to your specific situation. There were moments of genuine frustration - watching upload progress bars crawl to 94% and then hang there indefinitely, debugging remote repository connections, figuring out why builds were failing.

## Learning in Public

[[25-08-05 - Quartz - Gardening|Quartz - Gardening]] is the documentation of going back and forward in a hope it might help someone else get set up more quickly.  Also help me cement the journey in my own mind the real human experience of wrestling with unfamiliar tools.

## The Joy of Ownership

There's something deeply satisfying about having built this myself. When I hit "publish" now, I know exactly what happens: the content travels through Git to GitHub, triggers a build process on Cloudflare Pages, gets optimised and distributed to a global network of servers, and appears at my domain name with my chosen styling and structure.

It's mine in a way that the Obsidian Publish site never quite felt mine.  Although I'm worried I've introduced a bunch of friction in the process and the novelty will wear off.

This isn't because Obsidian did anything wrong, but because I didn't earn it. I didn't struggle with it, learn its intricacies, or solve its problems. It was just a service I paid for.

## The Path Forward

The real test, of course, will be whether I actually tend this garden or let it grow wild again. The technical infrastructure is just the beginning. The harder challenge is developing the discipline to regularly cultivate and share ideas worth growing.

But I'm optimistic. The act of building this system has already changed how I think about my notes and ideas. Knowing that there's a clear path from private thought to public garden makes me more intentional about which ideas deserve that journey.

And perhaps most importantly, the whole process reminded me why I love learning new things. The frustration of not understanding, the gradual accumulation of knowledge, the moment when disparate pieces click together into a coherent whole - that's the real satisfaction, regardless of the specific domain.

My digital garden is awake now, ready for whatever wants to grow next.

---

_If you're interested in the technical details of how I set this up, I've documented the complete process in the shed [[25-08-05 - Quartz - Gardening]]. It's probably more detailed than most people need, but that's rather the point - better to over-document than leave future gardeners stuck at 94% wondering what went wrong._