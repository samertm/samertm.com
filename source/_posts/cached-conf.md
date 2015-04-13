title: cached conf reflections
date: 2014-06-23
---

Cached Conf was a lot of fun! I came out of the "conference" with a ton of ideas, which normally doesn't happen!

#### Bret Victor - Inventing on Principle

<iframe width="560" height="315" src="//www.youtube.com/embed/PUv66718DII" frameborder="0" allowfullscreen></iframe>

Good talk! Bret is super into ideas, to the point where he feels like an injustice has been done to the world when an idea isn't able to grow. Which is interesting! And he showed off a bunch impressive visual programming things. Programming is about building and running a  mental model of computation in your head, but Bret thinks that there's no need to "play computer" if you have a computer sitting on your desk that you can harness it to do the heavy lifting for you. I think there's some truth to that, because I've tutored people before and everybody struggles with thinking about the state the machine is in. Having an immediate visual representation of that state would be an incredible tool for teaching. Maybe it would also help for other tasks, but I'd have to try it myself to form an opinion.

One of his big points is how the motivation for something is more important than the end result. People don't do significant things just because, they do them as the byproduct of chasing something else. For example, I am guided by a [reverence for life](http://en.wikipedia.org/wiki/Reverence_for_Life), but the "end results" of this are reflected in my diet and my views on [software](http://www.gnu.org/philosophy/free-sw.html). If you can only process the byproducts of someone's philosophy, you will not understand why they act the way they do.

#### Gary Bernhardt - Wat

<a href="https://www.destroyallsoftware.com/talks/wat">https://www.destroyallsoftware.com/talks/wat</a>

Funny talk, illuminates how having a complex set of coercion rules may as well be magic: if it's more clear to make a cast, the non-cast version may as well be undefined. Otherwise, you're just causing confusion.

#### Guy Steele - Growing a Language

<iframe width="420" height="315" src="//www.youtube.com/embed/_ahvzDzKdB0" frameborder="0" allowfullscreen></iframe>

Eye-opening talk! Guy Steele took every one syllable word as assumed knowledge and could only use longer words after he defined them to draw an analogy to using small programming languages. The meaning of his words were clear, but harder to express topics could be more awkward, and he had to define a significant set of words to use his "language". The trade off that he made was subtlety and expressiveness for clarity, and that's true for big vs small languages as well. When you're working in a large language, you can be more expressive, but only after a significant effort to learn the language and maintain that knowledge. And to draw an analogy to English, the biggest language I know: I use a lot of words where I'm not exactly sure of the meaning, but better express what I'm thinking. When your domain allows this sort of ambiguity, this is alright (or even desirable!), but software bugs thrive on "ambiguous" expressions that mean something different than what you've assumed. This complicates the task of debugging, because debugging is the act of going through every one of your assumptions about your code and finding the ones that don't actually hold, and there are many more corners for bugs to hide in big languages.

His big idea is that a programming language can only be successful if it starts small and grows with its users. Sounds reasonable. What he said about "growing" a language gave me a couple ideas for how I can make my version of Go more extensible, because Go's designers froze it at 1.0 as a pretty rigid language. An extensible Go would be fun to play around with.
