title: compilers - week 1
date: 2014-05-05 01:10
---

I'm on track so far! I got 100% on my lexer. Flex is a ton of fun to use -- you don't worry about the implementation, all your focus goes towards getting your `map[regexp]token` correct (that's Go syntax). Lexers, consider yourselves demystified!

The project was specified differently from how they did it at my old university. For the lexer, I was given the Cool manual, a reference for the tools, a reference lexer, and a slightly underspecified specification as the assignment. The hardest part was getting started. I needed to read a fair bit of material before I could figure out what the hell I was supposed to do with Flex's rules. Having the reference lexer was invaluable, and comparing it's output to my lexer's output made it super easy to make progress when the assignment instructions were unclear. And the grader dumped a buttload of failed test cases on me after I thought I was finished, which was also helpful :P. Going in, I was inexperienced at making software resilient to all possible input. Slowly making my lexer more and more robust was rewarding.

At my old university, our projects were spec'd out to an insane level of detail, and any ambiguity was considered a bug in the spec. We weren't given reference implementations or test cases. And I hadn't encountered any projects where we were expected to report errors for bad input. The difference may have been that I just never reached the "higher" level classes, but I have a hunch that Stanford expects a bit more from their students, too. It's a lot more fun to have to discover the answer to ambiguities on your own, in a twisted kind of way :P.
