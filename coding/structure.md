# Structure
Notes about coding in a structured way.

## The Wet Codebase
https://www.deconstructconf.com/2019/dan-abramov-the-wet-codebase
Dan Abramov discusses how a abstraction created to avoid duplicated code eventually turned into an unmaintainable monster with the passage of time.
Lessons:
  - Make sure you add high-level integration tests that don't care about your abstraction, so that major refactors can be done with confidence.
  - Delay abstracting until its clear and easy to understand, as abstractions are hard to explain
  - Be willing to in-line (un-abstract) your abstractions when they no longer make sense
  - Avoid Absolutes, teach the next generation of engineers about the trade-offs present in any `rule of thumb`

Quotes:
> ...we try so hard to avoid the spaghetti code that we create this lasagna code where there are so many layers that you don't know what's going on anymore at all.

> But if the new generation doesn't understand the trade offs and the reasons they came to these conclusions, they don't have the context to decide when it's actually a bad idea and how far can you stretch this

> And again, each of those individual steps kind of made sense. But if you lose track of what you were trying to do originally, you don't really know that you have a cyclical dependency or this weird thing that is growing somewhere to the side just because you don't see the whole picture anymore. And, of course, in real life, that's actually where the story ends because nobody wanted to touch the part of the code base and it just was stagnant for a long time and then somebody rewrote it. And maybe got a promotion. I don't know.  
