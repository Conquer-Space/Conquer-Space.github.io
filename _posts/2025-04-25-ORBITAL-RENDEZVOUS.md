---
layout: post
title: "Orbital Maneuvers II"
date: 2025-04-15
categories: ["dev-diary"]
tags: ["dev-diary", "orbital-mechanics"]
author: EhWhoAmI
---

It has been a while since the last update, but I've been hard at work!

Satellites can now execute basic orbital maneuvers, including plane matching, rendezvous, and moon landing.

We are able to land on the moon, and those ships show up on colonies. Returning back from the moon is also possible but I haven't implmenented that yet. But for now, most of the systems that we have are fairly robust, and extending the capabilities should be straightforward.

<video width="320" height="240" controls>
  <source src="/assets\media\2025\4\25\moonrendezvous.mp4" type="video/mp4">
</video>

I have written a Lambert solver as well, and the unit tests for the lambert solver all work. The code was referenced from [pykep](https://github.com/esa/pykep/blob/master/src/lambert_problem.cpp).

There is still some work that is needed to properly integrate this into the game. A potential use case is to refine the current orbital rendezvous calculations that we have.

Currently, we assume that the moon is in a circular orbit, match planes, and perform a basic Hohmann transfer to match the orbit. 

This works well for our current use case, but obviously there are a lot of limitations. It only works with a circular starting orbit, and since we are assuming that the moon has a circular orbit, the place we enter orbit is going to be unpredictable.

We could calculate when to perform a Hohmann transfer, and then use Lamberts to optimze the approach so that we can have a better

I think the current state of the game is good for a basic economic cycle, such as transferring resources to and from the Moon. I think this can give us good data on how our design of the economy works, and whether or not we need tweaks or not.

I am going to add a few resource deposits to the moon so that it makes sense to actually go to the moon and send resources back.

There are a few things that we need to accomplish, including interplanetary transfers, and a few bugs to squash, before we can properly call the systems complete, but I think we are in a good spot for now.

I will also write a proper unit testing framework for orbits, so that we can have a easy way to test out any fancy orbital manuevers.

The dream for the orbital mechanics system is for ships to autonomously travel to and from each the planets, and also between planets and moons, knowing when to transfer and not to transfer, or refuel and other things. Gravity assists would be cool to implement as well, but I'm not sure how bad that would be for performance.

In hindsight, I feel like all this could have been abstracted away, but I guess this gives a cool thing to do. Perhaps it could still be abstracted away and only left for combat, but for now I don't think we're to that stage yet..

I'm slowly getting back into the swing of things. I've been writing more code and doing more planning and reading.

I'm currently working and planning out the economy so that we get something that can simulate things relatively well and quickly but that is taking some time.
