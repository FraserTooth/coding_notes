# In Defence of Bad Code

Since graduating from Code Chrysalis, I've been "helping out around the house", teaching Foundations as a part-time instructor, as well as helping out with mock interviews for graduating immersive students. One question has come up repeatedly in various forms:

> Fraser, I want to write code that is the fastest/most efficient/cleanest solution possible - how do I do that?

And my response is usually something along the lines of:

> You don't.

So I wanted to elaborate on that.


## The Beautifully Terrible First Draft
  
There is a rule of thumb in software development called [The Rule of Three](https://en.wikipedia.org/wiki/Rule_of_three_(computer_programming)) which states that you probably don't need to abstract duplicated code until you have three duplications. This is primarily because if you abstract too early, you probably don't fully understand the problem so you'll end up doing it wrong. (Dan Abramov's talk [The Wet Codebase](https://www.deconstructconf.com/2019/dan-abramov-the-wet-codebase) is a great explanation on how this can happen in a project)

  
This is all centered around the idea that the first time you build anything, it will be imperfect, and that is **totally normal and expected**. Your first priority as a software engineer is to build stuff that is actually being used. Faffing around trying to make something perfect means that your stakeholders have to wait longer for anything to be done. Its far more important to get a bad first draft in the hands of your users, so that you can figure out what is worth improving. As long as this rough draft does the basic function its required for everyone is happy, so as long as it passes your automated testing its totally fine. You can always come back and fix it later if it actually becomes a problem.


A great example of this is a project I did during my first job. I was tasked with making our alerting system more useful, as alerts that came in were very basic and required a lot of investigation to understand whether or not they were important or not. I spent about a month creating an utterly beautiful set of reducers and adjustable triggers, with automatically generated graphs and loads of alert context - I am still rather pleased with what I made...but it never got used. It ended up getting stuck in deployment hell, due to some repo neglect, and by the time I managed to get it all sorted out, the business had moved on and there were other problems to solve. If I had managed to get something "a small improvement" out the door in a week, I could have gotten these deployment issues sorted out and been able to make iterative improvements over the following months.


Instructors at Code Chrysalis often say - `make it work, make it pretty, then make it fast` - this is true for the most part, apart from the fact that many companies never even get to the "make it fast" part. Primarily because...


## Time is worth more than money

If you work for a company with a typical cloud infrastructure, you can scale, in the context of slowish code this means adding more servers to handle the workload. The nice thing about scaling, is that it doesn't cost you any time, just money.
Developers aren't cheap, every hour they spend on a problem is money spent on that problem - but it also comes at an opportunity cost to all the other things that developer could have been working on. More features to attract customers, improving the design, admin tools to help your operational staff. Getting customers, making sales and keeping stakeholders happy is always going to be more important than the cloud spend. Customers do care about slow apps, especially in the frontend, but if you can quickly pay some money to solve the problem in the short term rather than losing developer time on making code changes, then they will get the credit card out every single time. 

You might think that this could also be solved by hiring more developers, but this only works if you hired the developers 6 months ago. Onboarding a new developer takes time and distracts all the other developers who could be working on other things, its not a short-term solution, growing a team is a long-term commitment. This also ties into the old idea of the [Mythical Man Month](https://en.wikipedia.org/wiki/The_Mythical_Man-Month) and [Brooke's Law](https://en.wikipedia.org/wiki/Brooks%27s_law) - which can broadly be summed up in the phrase `What 1 Engineer can do in 1 month, 2 engineers can do in 1 month`

Yes, this is unsustainable. There will come a point where a company will see that the cost of their cloud bill is far too high, and they need to spend some of that precious developer time on reducing it. But thats not something you really need to worry about, because...


## Its not your job to worry about efficiency

In general, it is a developer's job to write code and it is a product manager's job to help the developers to write the correct code. In an ideal world, the developers would only receive perfectly scoped work requests and they wouldn't need to ask anyones advice or for further context. Fewer distractions and meetings for engineers means more features in the pipeline - all good!
But, its rare to get enough information in a work request right? And we're a nosy lot aren't we? So we start asking about the business and we talk to all sorts of people and we "get ourselves involved" in the project at large. This can lead us to believe that _we know what would be good for the product_, but since we're not immersed in the wider context all day, this is often a misplaced sense of understanding. We get ourselves distracted.

Having a sense of agency can be great, but this is best expressed in the context of a "hack-day", where time is set aside for the engineers to improve things that they are passionate about. Some of the best internal tools come from these days - but its rare for something that actually makes money to come out of such an event.

Lets say you are fixing a bug, and you notice that there are some fundamental refactors that could be done to reduce the cost of this procedure by 33%. Sounds great right? Why wouldn't I just fix it? It'll only take me a day!  
But here are some things that might be happening, that only a PM or Engineering Manager would have view of:
 - That fix would cause a knock-on dependancy problem for another larger system
 - There is another refactor in the backlog that would save 5 times as much money and would solve this problem anyway
 - We have an upcoming contract negotiation with a client and want to get as many bugs fixed as possible to strengthen our position
