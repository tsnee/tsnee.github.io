---
title: "Animation"
date: 2024-03-19
---
#### 15:38 ET

My blog is one week old today.

I started chapter 4 of _WebGL Programming Guide_.
Rather than using a third-party matrix algebra package, I created my own, just powerful enough to do the examples.
After only three exercises I ran into Chrome's limit of 16 WebGL contexts active on a single page,
so I had to significantly refactor my display code.
Now it only shows one Canvas at a time.
I tried re-using the Canvas for all the examples, but event listeners and maybe WebGL objects like shaders started accumulating.
Rather than clean all that up manually, I decided just to delete the canvas and create a new one for each example.

While I was in there, I decided to show the original JavaScript implementations of the exercises side-by-side with my own.
That makes it easier to spot differences.

Chapter 4 is still all triangles all the time, but at least now they are starting to move. Animation!
