---
layout: post
title: "New Orbit System: Keplerian Orbits"
date: 2022-06-16
categories: ["dev-diary"]
tags: ["dev-diary"]
author: EhWhoAmI
---

Keplerian orbits have been added to the game.

Previously, though planets technically orbits, they were just a method to determine the static position of the planet. They existed on the x-y (according to OpenGL) axis, and did not move.

Now planets exist in 3 dimensions, and move according to (relatively) realistic orbital mechanics rules. The orbit style has modeled after Kerbal Space Program, where the orbit has a reference body, and bodies have a sphere of influence. This orbital system doesn't include the more complex forms of movement you can see in a N-body simulation, like barycenters or Lagrange points, but since it is deterministic, it works well for us.

To simplify the game, we have removed the wider galaxy, and changed the game to focus on only 1 star system: the solar system.

![Solar system image](/assets/media/2022/06/16/solarsystem-1.jpg)

Textures have been adjusted accordingly to properly represent the planets, thanks to [Erik](https://github.com/coderguy57) ([#151](https://github.com/Conquer-Space/Conquer-Space/pull/151)).

![Earth image](/assets/media/2022/06/16/earth-image.png)

As we can see above, we can see Earth, with the Moon, with fully formed textures.

All the distances are represented as real distances in OpenGL, thanks to log shaders ([#157](https://github.com/Conquer-Space/Conquer-Space/pull/157)).

The math is not super complicated, it's just rocket science after all.

We use [Keplerian orbits](https://en.wikipedia.org/wiki/Orbital_elements#Keplerian_elements) to represent our orbits.

The two documents that were relatively important to displaying the planets in orbit are [converting Keplerian orbits to cartesian orbits](https://downloads.rene-schwarz.com/download/M001-Keplerian_Orbit_Elements_to_Cartesian_State_Vectors.pdf), and [the opposite](https://downloads.rene-schwarz.com/download/M002-Cartesian_State_Vectors_to_Keplerian_Orbit_Elements.pdf). TheGreatFez also helped a lot with the math and the programming process, so a special thanks to his patience with helping me understanding all the math.

The orbits are not 100% well formed, because although we support planets leaving a sphere of influence, we do not support hyperbolic orbits, and entering sphere of influences. Hopefully that can be changed in the near future, but I am going to focus on economy for now.

There is also potential for the orbital system to get inaccurate over time, since double precision floating point numbers become less accurate at the multi-million kilometer range, but so far it works like a charm. We will think about it when we need precise orbital manuevers.

### The future
Transitioning from a galaxy wide game to a solar system scale game is a relatively large transition in the game.

This transition allows us to distinguish ourself from the relatively saturated 4x/grand strategy genre, because there are very few grand strategy games set in the solar system. (Maybe [Terra Invicta](https://store.steampowered.com/app/1176470/Terra_Invicta/)?)

The new restructured game will include interplanetary logistics, where you have to wait for the right launch window to launch to a planet. This should create interesting political and economic scenarios, so we can have interesting gameplay.

I will update the [features](/features.md) page and the home page as I slowly get more and more ideas as to what direction I want to bring the game.
