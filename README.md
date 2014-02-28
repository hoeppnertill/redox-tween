redox-tween – compiles with rustc 0.10-pre, 2014-02-26
===========

*This repository contains code that has not been properly tested yet, continue at the risk of doing stupid things while discovering that parts of this library don't work.*

## Introduction

Games and other applications often have a need to change values smoothly, without the need for a fully-blown physics system. This is where [Tweening][wikipedia] (Inbe **tween** ing) comes in. It allows to interpolate between numerical values in a lightweight way. 

[This YouTube video][youtube-juice] is an interesting example of how the addition of animations (via tweens) can change the feeling of a game. 

[wikipedia]: http://en.wikipedia.org/wiki/Inbetweening
[youtube-juice]: http://www.youtube.com/watch?v=Fy0aCDmgnxg

## Example
```Rust
use std::io::stdio::println;
use tween::to;
use tween::ease;
use tween::ease::InOut;
mod tween;

fn main() {
	let mut x = 0.; // the value which is changed

	// the object that performs the change
	// (subject, target, easing, mode, duration (any unit))	
	let mut tween = to(& &mut x, 100., ease::quint(), InOut, 10.);

	while ! tween.done() {
		// advance by 1 unit
		tween.update(1.);
		println(x.to_str());
	}
}

```

Another example can be found in `images.rs`. Compiling and running it *should* create `.ppm` files of all basic variations of tweens in `/tmp/`. If that directory doesn't exist for you, you should change the hardcoded path. (Yes, it should be an argument)

More complex examples will follow.


## Features

- Allows tweening of any type (via traits)
- Multiple easing equations:
 - Linear
 - Quad
 - Cubic
 - Quart
 - Quint
 - Sine
 - Circular
 - Back
 - Elastic
 - Bounce
- Easy to add own equations (just pass `fn(f64) -> f64` as `ease`)
- Easing modes `In`, `Out` and `InOut`
- Tween organization:
 - Sequential execution
 - Parallel execution
 - Pauses
 - Function execution
 - Repeated execution
- Three value access modes
 - via unsafe pointers
 - via `Cell`
 - via callback functions
- API built for conciseness

## Todo

- Direct `task` launching
- Making tweens `Send`able?

## Feedback and contribution

Feedback in any form is strongly desired. Either email me at `ubrccare.gvyy@tznvy.pbz` ([rot-13 that][rot13]), create an issue or ping me on IRC (nick: flan3002).

If you have an idea/need for a new feature or know how to fix a bug and want to be awesome, please contribute to this project.

[rot13]: http://www.rot13.com/

## Thanks

Many thanks to eddyb, cmr, bjz, kimundi, mindslight, hoverbear, sfackler, and others from [mozilla/#rust][irc]!
Also thanks to lifthrasiir from reddit for helping me with a `'static` problem.

[irc]: http://client00.chat.mibbit.com/?server=irc.mozilla.org&channel=%23rust

## Resources

For preview of the easing equations you may visit [easings.net][easings] for an overview of different easings. Note that `Expo` is not implemented at time of writing.

[easings]: http://easings.net/
