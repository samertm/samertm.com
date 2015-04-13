title: "proper way to return distinct types (in go)?"
date: 2014-06-10 12:37
---

Ran into a funny problem today with the parser. My parser would only handle s-expressions (like (these :D)), and I needed it to evaluate bare symbols as well. So if you ran, "(def meow 333)" (333 is the number of the half-devil, btw), and then "meow", I wanted my interpreter to return "333". My issue was that my parse function only returned Lists, and those are fed into eval. I couldn't just stuff the symbol (in the example above, the "meow" :3) into a list, because my eval function evaluates lists as function calls. I didn't want to return an interface type (void type for those familiar with C) because that seemed to obscure the purpose of my Parse: it should only return two things, a list or an atom.

My solution was to return multiple values (one reason why go is awesome) from the parse function, a list and an atom. When my parse bumps into a bare symbol, it returns nil as the list, and when it finds a list it returns nil for the atom. Czech the (simplified, sans-error-checking) code:

    func Parse(s string) (*list.List, *Atom) {
            strs := tokenize(s)
            t, strs := pop(strs)
            if t != "(" {
                    // handle bare symbols
                    return nil, &Atom{Value: t, Type: "symbol"}
            }
            ast := gen_ast(strs)
            return ast, nil
    }

And then in my main loop, I evaluate whichever of the two that is not nil:

    for {
            // blah code hidden
            input = getInputFromUser()
            ast, sym := parse.Parse(input)
            var a *parse.Atom
            if ast != nil {
                    a = eval(ast)
            } else {
                    // sym != nil
                    a = eval(sym)
            }
            fmt.Println(a.Value)
    }

But now that I think about it, it might be cleaner to just grab an interface bare and pass it in. Though it feels slightly wrong :O)
