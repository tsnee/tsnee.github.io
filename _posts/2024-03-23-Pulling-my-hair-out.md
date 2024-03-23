---
title: "Pulling my hair out"
date: 2024-03-23
---

#### 16:44 ET

S.L.A.S.H. works great! That's the good news.
I was easily able to use it just for matrix inversions, so the impact to my existing code was minimal.
The bad news is, I have spent the last several hours struggling over a weird bug in one of the last exercises in the book.
After racing through the end of chapter 8 and all of chapter 9 this morning, I have been stuck on "PickFace", a relatively
simple exercise for determining which face of a cube is clicked.
It's simple because there is a trick - as soon as the mouse is clicked, you can render a frame into the framebuffer
(but not apparently the screen) where each face of the cube has a distinctive value in its alpha channel.
When you get the RGBA values of the clicked-on pixel from WebGL, you can decode the alpha byte to determine which 
face was clicked. Then you draw the real frame, which is actually displayed on the screen.

[The example code](https://rodger.global-linguist.com/webgl/ch10/PickObject.html) works fine, so I can't blame browser bugs.
(I did find an error in [the Scaladocs for WebGLRenderingContext.readPixels](https://www.javadoc.io/static/org.scala-js/scalajs-dom_sjs1_3/2.8.0/org/scalajs/dom/WebGLRenderingContext.html#readPixels-fffff449)
that tripped me up for a few minutes, but no more.)
I worked over [my solution](https://github.com/tsnee/webgl-programming-guide-work/commit/844ecc6790d004fe9839a27f68b55696702218a4#diff-8aecd28a2d962aebbfb9124d59359e250f9e401beaf3d692bb2bb3fc51e9818f)
but for some reason `readPixels` returns values from the first face of the cube even when I click on other faces.
I have to click outside the cube entirely to get anything different from `readPixels`.

Sometimes something goes wrong with my sbt session (which might have more to do with metals than sbt, who knows) and I have to
quit sbt and IntelliJ and manually remove all my .bsp and .bloop directories and other metals files.
A `clean` by itself isn't enough. Until I do that, I get incorrect compilation errors, or even worse incorrect JavaScript.
This time I even tried running the build in GitHub actions, just to eliminate any possibility of a problem in my environment.
The bug is still there!

I have no idea what is wrong. If I had time, I would love to write a functional wrapper around the WebGL API whose types would
prevent me from putting the `WebGLRenderingContext` in a bad state, which is depressingly easy to do.
For now, I will just set my little project aside for now and pick up with the next exercise later on.
If I can face it tomorrow, I'll just delete the current exercise code and start over from scratch.
