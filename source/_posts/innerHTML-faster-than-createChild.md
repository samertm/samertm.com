title: "surprising: DOM manipulation by modifying innerHTML faster than using appendChild"
date: 2014-05-08 13:00
---

For my [multiplayer snake game](/project/snake), I needed to be able to modify an unordered list ("ul") by wiping all the "li" tags under it and generating them again for the scores of all of the snakes. My first idea was to create a string of "li" tags for all of my scores, and then set that as the innerHTML property of my "ul" tag. I'm vaguely familiar with the idea that DOM operations are expensive, though, and so I reached out to the DOM wizards I knew for more efficient ways of doing the same thing. They told me to try creating an "li" element and appending that to ul with appendChild.

So, I had two ways of doing the same thing, but I wanted to know which way was faster. The "appendChild" method seemed "closer to the metal" than setting innerHTML to a gigantic string, but modifying the DOM multiple times might be more expensive than doing it all at once. I knew I wouldn't be able to go to bed without knowing which technique was better, so I measured the speed of both, and the results were surprising!

All of the tests are run on Google Chrome 34.0.1847.134 on a Samsung ARM Series 3 Chromebook. The only browser tab running is the test. The times are rounded to the nearest thousandth.

##### Test results for the innerHTML method: ([all data](/res/innerhtmltrials.txt))

    For 30 trials with 100000 elements in the inner loop
    Average: 684.133 ms
    Standard Deviation: 45.281 ms
<img src="/img/innerhtmltrials.png">

##### Test results for the appendChild method: ([all data](/res/appendchildtrials.txt))

    For 30 trials with 100000 elements in the inner loop
    Average: 880.3 ms
    Standard Deviation: 280.129 ms
<img src="/img/appendchildtrials.png">

The innerHTML method is faster and more consistent than the appendChild method. The appendChild method has three outliers that spike to almost 2000 ms (!!!), where innerHTML is much compact. The standard deviation for appendChild is really high, and I tried to reign it in by increasing the number of trials, but that didn't have any affect on it.

The results for appendChild cluster right below 800 ms if you disregard the outliers, which is higher than the average time for innerHTML by about 100 ms.

Who would have guessed that the best way to make large changes to the DOM would be to set innerHTML to a gigantic string? :) I'm happy with this, because I think the innerHTML method is more clear.

If you want to try this at home, here are the files I used to test it: [test.html](/res/test.html) and [test.js](/res/test.js). If you notice anything interesting, send me an email (samer{@}this domain) because I'd like to hear about! Also, if there are any other ways of doing this, I'm interested in running more tests. :)

(Shout out to [Julia Evans](http://jvns.ca) for her awesome [introduction to ipython notebook and pandas](http://nbviewer.ipython.org/github/jvns/talks/blob/master/pyconca2013/pistes-cyclables.ipynb)!)
