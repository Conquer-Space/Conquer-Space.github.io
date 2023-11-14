---
layout: post
title: "Orbital Maneuvers I"
date: 2023-11-13
categories: ["dev-diary"]
tags: ["dev-diary", "orbital-mechanics"]
author: EhWhoAmI
---
A core part of the game will be orbital mechanics, so recently, I've almost completely overhauled the code for orbital math.

I managed to get basic orbital maneuvers working, including [Hohmann Transfers](https://en.wikipedia.org/wiki/Hohmann_transfer_orbit). 

So now, you can increase and decrease orbital altitude, and circularize your orbits with maneuvers.

For Hohmann transfers to work, your orbit needs to be circular, where the orbital eccentricity is below 1e-4.

<video width="320" height="240" controls>
  <source src="/assets/media/screenshots/hohmann_transfer.mp4" type="video/mp4">
</video>

Special thanks to [svapre](https://github.com/svapre) for implementing the colors you see in the orbit.

I'm still looking at [bi-elliptic transfers](https://en.wikipedia.org/wiki/Bi-elliptic_transfer), which can give slightly
reduced delta-v requirements for some types of tranfers at the cost of additional time. However, the circumstances that this
occurs is rare, and it is likely that it will be outside the sphere of influence of whatever body we are modelling.

Getting all the equations to work took a lot of time, because I didn't really understand how the math all fit together. However,
this is all fixed now, and hopefully, iterating upon orbital maneuvers will be a lot faster. 

There are unit tests to test as many aspects of the orbital maneuver as possible. I think I will be using a lot more unit tests for maneuvers so that we can ensure that the math is correct.

Next, I will be implementing plane changes, rendezvous, interplanetary transfers, and a Lambert solver.

After orbital mechanics, I think I will implement colonies, so that we can test out interplanetary logistics.
