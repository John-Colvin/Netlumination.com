---
layout: post
title: "Making a 2D JavaScript game engine: Part 2"
tags:
- javascript
- game engine
- animation
type: post
---
My first thought was to separate "physics" ticks from ui ticks, but several failing tests for the number of expected
physics ticks caused me to reconsider. I had a setInterval for 100 ticks per second:

```javascript
setInterval(function() {
    // ... physics tick
}, 10);
```

I thought the above code, would be guaranteed to fire 100 times per second. I assumed that even if the physics tick itself
 take more than 10ms, the next one would still start in time. I was very wrong. On my 10 year old Ubuntu laptop,
the above loop with nothing in it but an iterator would fire only 50 to 80 times per second in Fire Fox. So, I thought
 why not just run the physics loop immediately before the ui loop, thus running the physics loop as few times as
 possible? Since everything has velocities, the variable times between the ui loops shouldn't matter, since I can just
 use the actual time deltas.

Now that I've read [this](http://gamedev.stackexchange.com/questions/1589/fixed-time-step-vs-variable-time-step),
[this](http://gafferongames.com/game-physics/fix-your-timestep/), and [this](http://www.koonsolo.com/news/dewitters-gameloop/), I'm back
 to thinking that the phsyics loop deltas should be locked down. If for nothing else than reproducibility, since I do plan
 on having game play playback in the game engine, and also for debugging ease.
 
I also came across two fascinating John Resig artiles on JavaScript timers: 
[Accuracy of JavaScript Time](http://ejohn.org/blog/accuracy-of-javascript-time/) and 
[How JavaScript Timers Work](http://ejohn.org/blog/how-javascript-timers-work/)

Interestingly the same loop above works perfectly on Ubuntu FireFox on a newer 64 bit box. The difference hardware makes 
is fascinating. Burly computation power makes many problems go away. I think I'll stick with a setInterval for the game
render and a separate requestFrameAnimation for the UI render. I'll keep the game interval faster than the render update
so that I won't have to worry about interpolation.

---

### Notes

* general problem: mobile not supported 
sometimes not even rendering, often no controls
http://entityjs.com/games

* Decided to use AMD to for ease of writing
* AMD and qUnit: https://gist.github.com/4417534
