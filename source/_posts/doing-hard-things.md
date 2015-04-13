title: doing hard things, an experiment
date: 2014-06-15
---

I thought I was scott-free after figuring out the design of the parser with Aki yesterday, but it turns out that I was just getting warmed up.

I looked over go's grammar, which is thankfully available [online as part of go's spec](http://golang.org/ref/spec)... but the entire grammar has about 70 non-terminals! Most of those non-terminals will need a function to parse the associated tokens, a set of terminals to be checked to see if the upcoming tokens conform to the non-terminal's spec, and a data type representing the non-terminal.

The design phase is finished, and so what I'll be doing really amounts to a manual translation of the higher-level grammar into go code. It will require a large amount of focus, but not a lot of creative work.

I've never faced a task of this magnitude, so I'm going to try to set some rules/boundaries around how I spend my time:

1. Implement 5 non-terminals a day: I figure the most reliable way to make progress is to get small chunks done every day. Five is a fair amount, but it isn't dauntingly large, and it means I'll be finished in about two weeks. I will probably need to adjust this number as I build the parser.

2. Follow test-driven development: I've viewed test-driven development with suspicion in the past because of the number of people on the internet who sing its praises. Max has experience with it, though, and told me that TDD makes it easy to track your progress, gives you confidence in your code, and rewards you with passing tests as you write more code. All of those are useful things that will make it easier to maintain some momentum. I also like the fact that my first step will be writing a test, which is a small, tightly defined task, especially in contrast to implementing all the things involved in parsing a non-terminal. I've implemented the test for what I want to do next, and it was fun to think about what I wanted my program's output to be before I had written a line of code. It's not something I'm used to, and I feel like it was helpful. I'm afraid that having tests will make refactoring harder, but it will also give me confidence that a refactor didn't break anything, which is a trade-off I'm willing to make.

3. Mark my progress: I will mark my progress in the grammar, and note how many non-terminals I finished in my diary. Then, on days where I get less done, I'll be able to look over how much I've already finished and be happy.

4. Drink caffeinated drinks: Caffeine is my favorite drug. I have trouble focusing on things without caffeine, so I will allow myself to have as much caffeine as I want. I can see no way this can go wrong.

5. Listen to music: Listening to music is a double-edged sword. For most of my life, I never listened to music while working because it would drown out my inner voice, which makes it harder to reason about things. However, I recently learned that listening to music makes it easier to stay on task when I'm working on less interesting things, because my inner voice is usually bouncing off the walls in my skull, distracting me with irrelevant thoughts and bad jokes. I have experienced bouts of hyper focus with the combination of music and caffeine when working on mechanical projects that require a certain level of concentration. Hopefully I'll be able to take advantage of that on this project. Morrissey, give me strength.

6. Allow myself to be distracted: As long as I'm on track to finish five non-terminals, I won't allow myself to feel guilty for pairing with people on things that are completely unrelated.

I have my tests written for the non-terminal I'm implementing next. Here goes nothing!
