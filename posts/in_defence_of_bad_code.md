# In Defence of Bad Code

Since graduating from Code Chrysalis, I've been "helping out around the house", teaching Foundations as a part-time instructor, as well as helping out with mock interviews for graduating immersive students. One question has come up repeatedly in various forms:

> Fraser, I want to write code that is the fastest/most efficient/cleanest solution possible - how do I do that?

And my response is usually something along the lines of:

> You don't.

So I wanted to elaborate on that.


## The Beautifully Terrible First Draft
  
There is a rule of thumb in software development called [The Rule of Three](https://en.wikipedia.org/wiki/Rule_of_three_(computer_programming)) which states that you probably don't need to abstract duplicated code until you have three duplications. This is primarily because if you abstract too early, you probably don't fully understand the problem so you'll end up doing it wrong. (Dan Abramov's talk [The Wet Codebase](https://www.deconstructconf.com/2019/dan-abramov-the-wet-codebase) is a great explanation on how this happened in a project)

  
This is all centered around the idea that the first time you build anything, it will be imperfect, and that is **totally normal and expected**. Your first priority as a software engineer is to build stuff that is actually being used. Faffing around trying to make something perfect means that your stakeholders have to wait longer for anything to be done. Its far more important to get a bad first draft in the hands of your users, so that you can figure out what is worth improving. As long as this rough draft does the basic function its required for everyone is happy, so as long as it passes your automated testing its totally fine. You can always come back and fix it later if it actually becomes a problem.

A great example of this is a project I did during my first job. I was tasked with making our alerting system more useful, as alerts that came in were very basic and required a lot of investigation to understand whether or not they were important or not. I spent about a month creating an utterly beautiful set of reducers and adjustable triggers, with automatically generated graphs and loads of alert context - I am still rather pleased with what I made...but it never got used. It ended up getting stuck in deployment hell, due to some repo neglect, and by the time I managed to get it all sorted out, the business had moved on and there were other problems to solve. If I had managed to get something "a small improvement" out the door in a week, I could have gotten these deployment issues sorted out and been able to make iterative improvements over the following months.


## Time is Money

If you work for a startup with a typical cloud stack
