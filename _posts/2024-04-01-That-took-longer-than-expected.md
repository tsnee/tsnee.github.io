---
title: "That took longer than expected"
date: 2024-04-01
---

#### 12:27 ET

[Last week](../../03/27/Laminar-Redux.html) I wrote, "I predict that tomorrow I will be finished" with the exercises in the
_WebGL Programming Guide_.
Famous last words! It took me almost five days to finish the next-to-last exercise, displaying a Wavefront .obj file.
Part of it was dusting off my knowledge of Scala parser combinators to write code to read an unfamiliar format.
Part of it was the difficulty of debugging WebGL code. Can't put log statements in a shader! At least, I don't think you can.

If I wanted to do anything serious with WebGL, I would have to write a framework to protect me from the dumbest mistakes,
like using different spellings for attribute and uniform names in shader source and in Scala.js.
I imagine I could model the valid states of a WebGL rendering context as a state machine with transitions protected by the type
system. If it compiles, it works! I still have a lot to learn before I could take on that project though.
