title: "semicolon drama"
date: 2014-06-12 21:30
---

note: this is kind of a crappy blog post, most of which I wrote this morning, because I didn't get any work done after like 4pm, and I have a much clearer (though still not clear enough :) ) vision of how I want to my abstract syntax tree to look, and how I'm going to pass nodes to it (INTERFACES AND CHANNELS YO).

It's interesting having the history of a programming language available on the internet. I was reading about the post where go changed from semicolon-required-expect-for-these-special-cases, to lexical semicolon insertion. There seemed to be a significant number of people with complaints, who wanted to write in weird styles, or who thought that the lack of semicolons would mess with things. It's interesting to see so much hate for a feature that cleans up the syntax so much with no loss of clarity: if you need them, the semicolons are there for you!

I learned a nice lesson about the importance of compilers when participating in programming language discussions: rob (who announced the rule) specifically stated that the rule was a lexical one, not a semantic rule (he offered javascript's semicolon insertion rule, which was semantic and totally wonky, in contrast). He stated that this was because having the rule live in the lexing stage would be more clear than having it in the parsing stage. The fact that it's a lexing rule means that it's hard and fast: lexers shouldn't do special processing. And it was surprising how many people proposed that the special form

    a := (
          a,
          b,
          c
         )

not be covered by the rule, and be turned into

    a := (
          a,
          b,
          c
         );

instead of

    a := (
          a,
          b,
          c;
         );

This is only possible if the lexer is counting parentheses, and so what people were really asking for was another special case in the parser to handle things. And as someone writing a go parser, I appreciate rob & the gang for striving to keep the language as simple to implement as they could :)
