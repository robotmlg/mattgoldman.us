---
layout: post
title:  "Mysteries of the Code: Episode I &ndash; The Phantom Char"
date:   2016-04-09
author: Matt
categories: mysteries of the code
---

It was a night like any other: I was procrastinating on my programming homework 
by working on another project when my flatmate came over.

"Hey Matt," he said, "you're good with C.  I'm having some trouble printing a 
string."

"Okay, what's the problem?"

"So the string is a domain name, but instead of dots, it has a number telling
you how many characters are in the next chunk of the name.  So like 
`3www6google3com`.  So my question is, how do I convert a character into a number?"

"Ah, that's easy," I said, "just subtract a `'0'` character."

"What?" he asked.  He's not a C programmer, and so didn't know this simple trick.

"ASCII has the digit characters arranged sequentially, so the `'3'` character is 
three larger than the `'0'` character.  So if you subtract a `'0'` from a `'3'`,
you just get `3` out."

Through some more explanation and description by my flatmate, I figure out that
it's not actually a `'3'` character, but a character with the value `3`.  No
`'0'` subtraction required!

"Okay, so you get the first character, spit out that many characters, you know
the next one is a number, so you repeat that until you hit the end of the string.
What's the problem?"

"Well," he said, "I'm trying to print out `test.domain.com` but it's not printing
the second `t` in `test`."

"Ah ha!" I said.  "You're probably trying to print a character that messes with
your text.  Like, there's a backspace ASCII character that deletes the last
character printed."

"What&#8253;"

"It goes back to when we had teletypes instead of terminals.  Not important right
now.  So, your last character before `domain` gets deleted.  `domain` is 6 
characters, so I bet the backspace character has value 6."

I look up an ASCII table.  "Aw darn, the backspace character is value 8, not 6.
Must be some other problem.  Let me take a look at your code."

"Oh wait," he said.  "It's not `test.domain`.  It's `test.mydomain`."

`mydomain`.  8 characters. So the prefixed `8` was causing the last `t` in `test`
to get deleted.  Another mystery solved.  I went back to my project and my
flatmate went back to his.


## The End?

Tune in next time for more...

## Mysteries of the Code
