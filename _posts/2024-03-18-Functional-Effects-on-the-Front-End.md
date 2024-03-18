---
title: "Functional Effects on the Front End"
date: 2024-03-18
---
#### 07:21 ET

I really had my heart set on using functional effects in my Scala.js code.
Calico is very promising, but does not yet support all the functionality I need.
I re-examined Laminar to see if it had started supporting ZIO or Cats Effect. No dice.
[Outwatch](https://outwatch.github.io/) supports both ZIO and Cats Effect! It uses a different approach than Laminar and Calico
(virtual DOM) but I had no reason to think that was a drawback.

It took me a little while to figure out how to use npm and Vite instead of Yarn and Webpack.
A bigger issue was that I could not figure out how to set the width and height of a Canvas element.
Outwatch's standard "width" and "height" modifiers use CSS, which makes a Canvas look stretched.
Another issue: Outwatch's Canvas does not have `getContext`, so I had to get access to the underlying
`org.scalajs.dom.html.Canvas`.
The deal breaker was the amount of complexity I added to my code. 

I am loath to blame Outwatch, since it is fairly simple and easy to use. It's probably fine for the standard dynamic HTML
use case. My use case though is WebGL, and Outwatch does not appear to have any support for it at all.
To implement my own support requires access to the real (not virutal) DOM element, which is only available in a callback,
`onDomMount`. What if you want to update the WebGL context from another callback like `onClick`?
The only simple solution I could find was to call `getContext` in each event handler.
That's a perfectly valid thing to do, but it didn't appeal to me.

It was with a heavy heart that I decided to set aside functional effects for now.
I was easily able to avoid the use of `var`s by storing state in JavaScript arrays, which are of couse mutable.
It isn't as ugly as I had feared, although I still wish for a better solution.

#### 14:06 ET

Finished chapter 3 of the WebGL book. I made the presentation of the examples a little nicer.
Next challenge: use GitHub actions to publish that presentation somewhere.
