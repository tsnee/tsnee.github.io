---
title: "Second Chapter"
date: 2024-03-11
---
#### 19:18 ET
Today I finished [doing the exercises in chapter 2](https://github.com/tsnee/webgl-programming-guide-work/tree/main/src/main/scala/io/github/tsnee/webgl/chapter2)
of _WebGL Programming Guide_. Not completely though - the last two examples involved storing the location of mouse clicks in a
global mutable array. Since the whole point of this exercise is to write front end code in a purely functional way, I decided
to just draw the most recent click and not explicitly maintain any state.

I introduced Cats Effect thinking `cats.effect.kernel.Ref` would solve my problem. My browser kept stopping whenever the
Cats Effect code referenced `js.Dynamic.global.process`, which it appears to do everywhere. With help from Typelevel's Discord
community I realized that the current code wraps access to that object, which does not exist in the browser environment, in a
`Try`. That's perfectly legal, but I had configured Chrome DevTools to stop even on caught exceptions, not just uncaught ones.
Once I stopped doing that, Cats Effect worked fine.

The bigger problem was that I wanted to wrap all side-effecting code in an effect Monad like `cats.effect.IO`. That's fine for
the main body of code, which can bubble up `IO`s all the way to the end of the world, since my main object could implement
`cats.effect.IOApp.Simple`. It did nothing for event handlers though since they are called asynchronously. Even if I refactored
the code to remove all WebGL calls from the mouse click handler, I would still have to access the `Ref`, which is impure. The
only thing I could think of was to wrap the handler in an `IO` but then to immediately call `unsafeRunAndForget` on that IO.
What would be the point of that?

As much as I had wanted to do these exercises with as few external dependencies as possible, I reluctantly came to the
conclusion that I could not create real front ends in a purely functional way without using another library. The two I know of
are [Laminar](https://laminar.dev/) and [Calico](https://www.armanbilge.com/calico/). I have had great experiences with Laminar
in the past, but I don't believe it comes with support for any functional effect system out of the box. If I wanted to use
Laminar I would have to pretend that the WebGL API wasn't a tangle of side effects, which simply isn't true. Maybe one day I
will write my own pure functional wrapper around WebGL, but I have to learn it first. In the meantime I can at least lift the
WebGL calls into a `ZIO` or an `IO`.

Enter Calico, a library inspired by Laminar but with explicit support for Cats Effect. I have no experience with it, but a
great respect for its author. I don't believe it supports WebGL in any way, but as long as it allows me to return an `IO` from
an event handler, it should fill the need.
