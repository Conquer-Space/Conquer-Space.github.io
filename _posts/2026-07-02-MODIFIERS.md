---
layout: post
title: "Modifiers"
date: 2026-07-02
categories: ["dev-diary"]
tags: ["dev-diary"]
author: EhWhoAmI
---
So I added modifiers to the game to allow some values to get a modifier bonus or malus. There are two types of modifiers, additive and multiplicative. Additive modifiers is just a basic addition to the preexisting value, while a multiplicative modifier sums up all the modifiers and then multiplies that value with the base value.

This modifier system is a way to be able to enable some values to be changed in a trackable and configuratble method, so this was the way to go about it.

There are a few limitations with the system: one being that modifiers that rely on another value are just not possible at all.

To define a modifier, you can go to the game's modifier value, and add a modifier value like how you would add a value in any other entity or value. I will try to create a way to add documentation/a UI so that is easier to keep track of the types of modifiers that exist in the game.

A modifiable value will act exactly like a double, so in the code, there is not much difference in using a modifiable value.

I would also like to talk about my philosophy around modifiers. One of my criticisms of Paradox-style grand strategy games is that it ends up being a modifier stacking exercise. I do understand that stacking modifiers can be pretty fun, and from a development standpoint, it is also relatively straight forward. Adding more modifiers is a pretty simple operation, and it is also easy to balance them.

But, one of the philosophies I would like to carry forward with the game is the necessity for continued improvement and investment in capital, and I don't think the modifier system would capture the full scope of what I want to portray.

I also don't want to deal with modifier spam because it doesn't feel very realistic, and also kind of feels like a slop.

As a general idea, I think I will think carefully on the use of modifiers, and how to use them meaningfully, so that there is less of a slog on trying to figure out what each modifier does. Each modifier should have a clear and straightforward benefit or malus, and the use of complex modifiers should be limited.