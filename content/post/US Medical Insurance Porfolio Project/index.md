+++
toc = true
readingTime = true
draft = true
image = ''
date = '2025-09-06T11:54:52+02:00'
title = 'US Medical Insurance Portfolio Project'
description = 'A very fun, hands-off data analysis project.'
tags = [
    "Python",
    "Analysis",
    "Project",
    "Programming",
]
categories = [
    "Data Science",
    "Project Showcase",
]
series = [""]
aliases = [""]

+++

# Portfolio project : US Insurance data Analysis.

## Intro 

I had a blast with this project! 
It was fun to do and I learned a lot, but most importantly, I practiced by challenging myself. This project exemplifies why a platform like CodeCademy can be an exceptional way to learn. 

Let me explain.
The prject begins with a CSV of insurance data, containing 1300+ rows of these columns: [age, sex, smoker status, bmi, region, children, charges]. The ‘charges’ being the most important variable here : this the yearly cost of medical insurance for someone.

The only vague instruction comes in the introduction of the project ; 
> “Now, **you** figure it out.”  -CodeCademy, (heavily paraphrased)

That’s it. You have the file, now decide the rest. 
There is a kanban board of vague and broad ‘tasks’ to do, like “importing the necessary libraries” and “having a look at the data”. 
Not only is it vague and kinda obvious but it’s also a gimmick; a list would have been as good. 
You have a data set and a broad mandate : analyse it, which invites the question, (side-note : no, it doesn’t “beg the question”. That would be a misuse of that expression, I’ll let you get down that click-hole for yourself.) It induces the question: what would be pertinent to find out in this case? What should I try to figure out, and more interestingly, what do I *actually* want to know? 

That’s the magic: you’re not doing an exercise anymore, trying to tick one more checkbox before lunch, you’re *actually* trying to figure something out. Oddly enough, you can only succeed: you set out the objectives yourself, so the only way to fail would be to abandon before that. Getting help is not just allowed, it’s expected. 
I guess this is similar to the thrill of the hunt, of jumping into trouble, confident you’ll get out of it somehow. 
Fun stuff.


## What I wanted to know and what I found out:
I wanted to know the obvious things: 
- How expensive is smoking to healthcare? (Extremely expensive : 400% more). 
- How expensive is A high BMI? (expensive, but that much as I expected.)
- Children? (Surprising, not much at all.)
- Are some regions more expensive? (Weirdly,Yes. East is worse than west, south is worse than north, so southeast is the worst.)
- Age? (older is worse, as expected.)

This list is of all the obvious relationships to look at, and they *are*, but somehow they feel like *mine* while coding, so it made me try to do things the way i would actually do things if no one was watching over my shoulder. Oddly enough, I am now sharing what I did, with some sense of pride I would not have if I had followed precise instructions. 


### Cool things 
I did a good job, if I may say so myself. 
I had a look at the “example solution” provided by CodeCademy and I am not impressed. It stops just as it’s getting into the interesting stuff, to begin with, but mostly, they don’t do a finer analysis than I did, and they do it *less* elegantly.

For instance, I’m proud proud of a function I built (compare_charge_per_var) that matched any variable in the dataset to charges and returned the average charge for each value of that variable. It allows to compare the average price for men/woman, smoker/non-smoker, etc... 
Pretty nifty and efficient. It even prints in a readable manner. And I built it only because I wanted to. 
I could have copied and modified some loops I had already done, but I was confident I could build the function, and it seemed like an interesting challenge that would teach me something. The broad mandate of the project encourages leaving the easy road to forge a new path into the wild. 
So I did, and discovered I’ve had the same idea as a thousand others, but you know what: I had it too. On my own!

Now, the function gets useless for variable with a lot of categories (like age and bmi) because the results are not sorted (solvable), but mostly because they are not grouped by categories, which is harder to solve. So it’s not perfect but I can imagine a helper function that would calculate the ranges of each variable in a dataset then automatically build categories for that range, name them, and feed that into the function. It’s probably too ambitious for me right now, but it’s certainly enticing. 
I might crack that nut, given enough time, but it simply wasn’t worth it when I can make bespoke categories for the two problematic variables, as I did.

Something I might actually do is instead of always comparing to charges, I could compare to any other arbitrary variable. 
Compare, say, age with kids, or smoker-status and kids (I did that one for fun : there is no correlation I can see.)

Another example of a self imposed learning moment fueled by curiosity was learning about the Counter() and  Sorted() method. 
Counter is useful to have an idea of the ranges of values in a variable. How high do ages go for instance. Of course, the result can be messy to read. So there is the Sorted() method. 

Beyond learning about the methods themselves, it shows the broad scope of methods, and the abundance of libraries in python. There is python, but then all the python “plugins” .

## Next

There we quite a few moments when I wanted to *see* the data. Graphing variables, their relationships would be quite useful, and not just for generating “actionable insights”, just a tempory tool while exploring data. 
For instance, when looking at bmi, it would be very nice to just plot all the data points on a curve and look at the shape. I sorta did that using the Sorted() method, to order everything, but it’s still not very nice. 

I looked into it obviously, and it’s done with pandas, which is the very next module in the course. Nice.
