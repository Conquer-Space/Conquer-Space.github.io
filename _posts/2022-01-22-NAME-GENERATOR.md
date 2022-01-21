---
layout: post
title: "Name Generator"
date: 2022-01-22
categories: ["dev-diary"]
tags: ["dev-diary"]
author: EhWhoAmI
---
I have added a name generator to the game. Although it isn't sophiscated, it does allow us to add some flavor into the game, for planet and city names, and the like.

The way it works is rather simple.

The file format is a hjson file, and looks like this:
```
{
    name: [generator name]
    rules: {
        [rule name]: [format]
    }
    [syllable name]: [
        [Array of syllables]
    ]
    [syllable name]: [
    ]
    // more syllables
}
```

The format string is processed in fmt, so it would look like this: `{[syllable 1 name]}{[syllable 2 name]}`.

For each syllable, a random syllable will be selected from the array, according to the random generator
that you provide, and formatted into the string. So you can add spaces and other text into the

In the future, I would like to have a more adaptable naming scheme capable of naming cities and other things
after people and the events, but for now a simple name generator would do.
