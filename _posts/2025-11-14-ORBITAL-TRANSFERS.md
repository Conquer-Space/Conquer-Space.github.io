---
layout: post
title: "Earth-Moon Orbital Transfers"
date: 2025-11-14
categories: ["dev-diary"]
tags: ["dev-diary", "orbital-mechanics"]
author: EhWhoAmI
---

After a great amount of effort, I was finally able to get orbital transfers to work!


<iframe width="560" height="315" src="https://www.youtube.com/embed/5LvDKe2Wvpk?si=6uZWzzXzvvMOi-WX" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

In this video, we can see ships move back and forth between the Earth and Moon, each carrying various goods, all automatically.


We have the fake "Armstrong" moon base as a temporary base to test out our transfers. We have some goods in demand that both sides want but don't have, which causes ships to go back and forth between each body.

We don't have the ability to transfer between planets yet, but I don't forsee this to be a huge undertaking as we have enough infrastructure and algorithms that we can just string them together with minimal math.

We still need to add ways for the spaceports to actually consume and eject goods, but that is coming up soon in the coming few PRs.

Orbital transfers are not very accurate, which is tracked by [#312](https://github.com/Conquer-Space/Conquer-Space/issues/312). Since we only calculate our
maneuver once, our maneuver's time is incorrect, so we will need an iterative algorithm to fix it.


In the next update, I will be talking about how the economic model works.
