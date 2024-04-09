---
title: "Python - February"
date: "2015-04-28"
categories: 
  - "one-language-per-month"
coverImage: "img.png"
---

Yep, I know everybody and their grandmother knows Python. I've modified Python code of sorts over the year, but I've never actually looked at what it would be like to write Python. The [One Language per Month](/blog?category=One%20Language%20per%20Month) challenge was a good opportunity to fix this.

\>

![](https://images.squarespace-cdn.com/content/v1/52375b95e4b030ffaec4c1f9/1423913051216-7LJIGP7QDVEABWUEFC27/image-asset.png)

Python has been around for a long time. It was originally released in 1991 and development on it started a few years earlier. It's a very mature language with a huge ecosystem of libraries, tools, and user base.

Python is an interpreted language that can be compiled into bytecode which then is ran in a virtual machine. The bytecode is then either interpreted or compiled, typically just-in-time, at runtime. The official runtime engine, CPython, interprets the bytecode. If you want to learn more, check out [python.org](https://www.python.org/)

The learning curve for Python was non-existent. Very easy to learn, quick to use. Quite handy!

Python has a nice generator pattern, which makes it very straightforward to create functions that stream responses out from that function onto the next step of processing. I guess the easiest way to conceptualize this is to image a function that returns a list, but instead of that function collecting a the complete list before returning, each element added to that list is immediately processed by the original caller, after which the generator function continues from where it left off. This helps write memory efficient code while avoiding complexity in the codebase.

However I found the lack of true concurrency in the language quite disturbing. Some runtime engines do allow for this, but the default engine, CPython, does not. This creates two issues: fragmentation and issues with cross-platform support.

Another thing I disliked in Python was how whitespace in interpreted. For some reason, I really dislike programming languages using whitespace as control characters. Typically code blocks are encased in braces or begin / end statements but in Python, a code block is defined by the indentation of the code. For instance in an if statement, the code block controlled by the statement is written prefixed by space characters before each line of code.

```
if foo == bar:
  print "Hello World"

```

For some reason or another, I just find that distasteful. However it can be argued that this teaches people to do indentation correctly right from the start. And I do like correct indentation.

I think I'll definitely find many uses for Python in the future. It matched my expectations: a fast language to do advanced scripts and stateless server processes. I just have to remember to push myself to use python instead of relying on ye olde method of shell scripts.

PS. This is very late, very very late, but I'm going to try to keep to my goal. While it may not be exactly one language per month, I'll strive for 12 languages within the year.
