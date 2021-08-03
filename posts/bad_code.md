# Bad Code

Since graduating from Code Chrysalis, I've been "helping out around the house", teaching Foundations as a part-time instructor, as well as helping out with mock interviews for graduating immersive students. One question has come up repeatedly in various forms:

> Fraser, I want to write code that is the fastest/most efficient/cleanest solution possible - how do I do that?

And my response is usually something along the lines of:

> You don't. You should write bad code.

So I wanted to elaborate on that.


## The Beautifully Terrible First Draft
  
There is a rule of thumb in software development called [The Rule of Three](https://en.wikipedia.org/wiki/Rule_of_three_(computer_programming)) which states that you probably don't need to abstract duplicated code until you have three duplications. This is primarily because if you abstract too early, you probably don't fully understand the problem so you'll end up doing it wrong. (Dan Abramov's talk [The Wet Codebase](https://www.deconstructconf.com/2019/dan-abramov-the-wet-codebase) is a great explanation on how this can happen in a project)

  
This is all centered around the idea that the first time you build anything, it will be bad, and that is **totally normal and expected**. Your first priority as a software engineer is to build stuff that is actually being used. Faffing around trying to make something perfect means that your stakeholders have to wait longer for anything to be done. Its far more important to get a bad first draft in the hands of your users, so that you can figure out what is worth improving. As long as this rough draft does the basic function its required for, everyone is happy. And, as long as you write automated tests to guarantee the current (bad) behaviour of your program, it will be easier to change, allowing you to quickly come back later and fix it if it actually becomes a problem.


A great example of this is a project I did during my first job. I was tasked with making our alerting system more useful, as alerts that came in were very basic and required a lot of investigation to understand whether or not they were important or not. I spent about a month creating an utterly beautiful set of reducers and adjustable triggers, with automatically generated graphs and loads of alert context - I am still rather pleased with what I made...but it never got used. It ended up getting stuck in deployment hell, due to some repo neglect, and by the time I managed to get it all sorted out, the business had moved on and there were other problems to solve. If I had managed to get something, maybe just a "small improvement", out the door in a week, I could have gotten these deployment issues sorted out and been able to make the cool improvements I wanted over the following months.


Instructors at Code Chrysalis often say - `make it work, make it pretty, then make it fast` - this is true for the most part, apart from the fact that many companies never even get to the "make it fast" part. Primarily because...


## Time is worth more than money

If you work for a company with a typical cloud infrastructure, you can scale, in the context of slowish code this means adding more servers to handle the workload. The nice thing about scaling, is that it doesn't cost you any time, just money.
Developers aren't cheap, every hour they spend on a problem is money spent on that problem - but it also comes at an opportunity cost to all the other things that developer could have been working on. More features to attract customers, improving the design, admin tools to help your operational staff. Getting customers, making sales and keeping stakeholders happy is always going to be more important than the cloud spend. Customers do care about slow apps, especially in the frontend, but if you can quickly pay some money to solve the problem in the short term rather than losing developer time on making code changes, then they will get the credit card out every single time. 

You might think that this could also be solved by hiring more developers, but this only works if you hired the developers 6 months ago. Onboarding a new developer takes time and distracts all the other developers who could be working on other things, its not a short-term solution, growing a team is a long-term commitment. This also ties into the old idea of the [Mythical Man Month](https://en.wikipedia.org/wiki/The_Mythical_Man-Month) and [Brooke's Law](https://en.wikipedia.org/wiki/Brooks%27s_law) - which can broadly be summed up in the phrase `What 1 Engineer can do in 1 month, 2 engineers can do in 1 month`

Yes, this is unsustainable. There will come a point where a company will see that the cost of their cloud bill is far too high, and they need to spend some of that precious developer time on reducing it. But thats not something you really need to worry about, because...


## Its probably not your job to worry about efficiency

In general, it is a developer's job to write code and it is a product manager's job to help the developers to write the correct code. In an ideal world, the developers would only receive perfectly scoped work requests and they wouldn't need to ask anyones advice or for further context. Fewer distractions and meetings for engineers means more features in the pipeline - all good!
But, its rare to get enough information in a work request right? And we're a nosy lot aren't we? So we start asking about the business and we talk to all sorts of people and we "get ourselves involved" in the project at large. This can lead us to believe that _we know what would be good for the product_, but since we're not immersed in the wider context all day, this is often a misplaced sense of understanding. We get ourselves distracted.

Having a sense of agency and involvement in your work can be great, but this is best expressed in the context of a "hack-day", where time is set aside for the engineers to improve things that they are passionate about. Some of the best internal tools come from these days - but its rare for something shippable to come out of such an event.

Lets say you are fixing a bug, and you notice that there are some fundamental refactors that could be done to reduce the cost of this procedure by 33%. Sounds great right? Why wouldn't I just fix it? It'll only take me a day!  
But here are some things that might be happening, that only a PM or Engineering Manager would have view of:
 - That fix would cause a knock-on dependancy problem for another larger system
 - There is another refactor in the backlog that would save 5 times as much money and would solve this problem anyway
 - We have an upcoming contract negotiation with a client and want to get as many bugs fixed as possible to strengthen our position
 - The competition just released their "killer feature" and we need to get our version out before people start asking why we don't have it!

The big picture might not be in your view, and thats fine - being given space to focus on the specific work that needs done means that you're probably not going to be kept up-to-date on all the myriad other problems being juggled at any one time. Its not your job to worry about whether you, as a company, are spending too much money on your cloud bill. If you see something that could be fixed, just write what you've learned in a ticket and let your Product Manager know. It may well end up being really important for the problems they are currently facing - but thats for them to decide.

Besides, you don't even know if they understand the problem you're trying to explain. Hell, your other developer colleagues might not understand the problem. Communicating the exact concern can be really hard, and one thing that can make this a lot easier is getting into the habit of...

## Writing for 5 year olds

Imagine your colleague assigns you as a reviewer on their Pull Request. You haven't spoken about the work and all the Pull Request says in the description is:

```markdown
Combines all the check messages into one output status `Pass/Fail` and a list of error message strings
```

This seems a bit basic, but you think that maybe the commit history will explain a bit more. Unfortunately, its not very helpful - you see they've made a change to a few files and some test files, a new `IF` statement seems to check some value in an object. It doesn't look _too_ complicated, but you don't really understand it either...  

Really frustrating right? Now you've got to sit down **and really read this damn code**. You've got to read all the old code, and all the new changes, look at the variable names, look at the tests as changed, and try to figure out what was actually changed and why. This can take a really long time, especially so if your colleague has used some fancy new language features or maybe they've tried some interesting recursive logic. Maybe something like this:

```python
def run_checks(inputs):
  
  checks = [_has_x(input), _has_y(input)]

  def reduce_checks(reduced_result, check_result):
    result = reduced_result[0] if reduced_result[0] is False else check_result[0]
    error_list = reduced_result[1]
    if check_result[1]:
        error_list.append(check_result[1])
    return result, error_list

  return reduce(reduce_checks, checks, (True, []))
```

WHAT IN THE FRESH HELL IS THAT !?!?! (_disclaimer: I wrote this, **I** thought it was **very** clever_)

So of course, a lot of your PR comments are probably going to be asking questions: `what is this check actually checking?`, `what does this acronym mean?` which means that you're spending lots of time writing questions, and they're spending lots of time answering them.

Now imagine you ask a bootcamp student to say what is wrong with this code, they look at it and think its impressive! Oooh, look at the `reduce` function, very fancy. They think the code is clever, and since its written by my colleague who I respect it must be correct!
So maybe they suggest some improvements like:
 - Use type hints to clarify the input and output structure
 - Use comments
 - Rename variable

But all of these improvements are ADDING code. What about code we could just...take away? The question here aught to be "why isn't this code simple?". 
This is what I eventually wrote (_after some feedback_):

```python
def run_checks(input):
  
  checks = [_has_x(input), _has_y(input)]

  result = True
  errors = []
  for check in checks:
    if not check.passed:
        result = False
        if check.error:
            errors.append(check.error.value)
                
  return result, errors
```

I did add type hints and comments after this, but I really didn't need to add much, because its quite straightforward. A loop and a couple of `IF` statements.
I used the features of Python that lend themselves to **readability**. `for check in checks` - its a simple loop, but it reads like regular english. There is a reason `for...of` is the first loop we teach in the Code Chrysalis beginners Foundation course, its readable, arguably, by a 5 year old.
And therefore, **it is safe code**, we can be much more confident that our colleagues will be able to properly review our code and ensure that we haven't made any (totally normal) human errors. Simple code is easier to typecheck. Simple code is easier to refactor. Even if you have some big discussion on Github or Slack about how your clever solution works and everyone agrees that you're a big clever clogs - that conversation isn't in the code, and you'll cause problems for the poor sod who has to try and understand your _genius_ in 7 years time.

This idea extends to all sorts of things - documentation, PR descriptions, emails, backlog tickets, presentations. Whenever you write something, sit back and think...could this be simpler? Could I say this in fewer words? (as I will inevitably do several times with this post 😆) Everyone will thank you for it.


## In Conclusion

So, in summary, you aren't going to write efficient software because:
1. You probably don't know what the perfect solution looks like yet.
  - _The Rule of Three_ 
2. You don't have time to build the perfect solution.
  - _Brook's Law_
3. You don't have to worry about the monetary cost of your silly code (until you're told to).
  - _AWS credits go brrrrrrrr_
4. You shouldn't, because dumb code can be properly reviewed by your peers.
  - _Explain it like I'm 5_

