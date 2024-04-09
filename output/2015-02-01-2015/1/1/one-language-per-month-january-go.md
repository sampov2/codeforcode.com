---
title: "Go - January"
date: "2015-02-01"
categories: 
  - "one-language-per-month"
coverImage: "img.png"
---

[

\>

![](https://images.squarespace-cdn.com/content/v1/52375b95e4b030ffaec4c1f9/1420991709327-YVB6TTUFSYVMS999ID9U/image-asset.png)



](http://golang.org/)

[](http://golang.org/)

Go seems to be getting some [traction](https://code.google.com/p/go-wiki/wiki/GoUsers) and is [rising in popularity](http://www.google.com/trends/explore#q=%2Fm%2F09gbxjr&cmpt=q&tz=) either of which would by itself be a good enough reason to see what the fuss is all about. This made Go a no-brainer choice as one of the languages in my [One Language per Month](http://codeforcode.com/blog/2015/1/1/one-language-per-month-2015) challenge of 2015.

The basic syntax is immediately familiar to anyone who knows C. Despite the familiar syntax, Go has a learning curve. It uses a some concepts that, while not entirely unique, are not that usual in programming languages. Here's the obligatory Hello World:

`   ``` package main  import "fmt"  func main() {   str := "Hello World"   fmt.Println(str) } ```   `

Go felt kind of like watching Back to the Future 2 - you're getting shiny new concepts like hoverboards and cool sneakers (=[defer](http://blog.golang.org/defer-panic-and-recover), [go](http://blog.golang.org/go-concurrency-patterns-timing-out-and), and [channels](http://golang.org/doc/effective_go.html#channels)), but they are presented to you in a world also littered with anachronisms that date back to the time the plot was written.

## **The good**

Starting threads in Go is a breeze. You can just prefix any function call with _go_ and that function call will execute in a separate thread while current execution scope will immediately continue. Channels are special objects which work as command or message queues that can be used for communicating between different threads. Combining these two makes it relatively easy to do parallel computation. Using this pattern is very different from classical mutex mechanisms like semaphores, so it takes a bit of effort to get comfortable with it.

I also really like _defer_. This keyword is applied similarly to _go_ and adds the function call to a stack of functions that will be called once the current function exits. Using defer to, for example, release resources allocated within the function, keeps code much cleaner than for example try-finally or try-with-resources in Java.

Package management is built in the language. This has been typically provided by an 3rd party in most languages I've worked with. Think Maven in Java, NPM in NodeJS, Gems for Ruby. It's very encouraging to see that ecosystem support is built into languages.

The switch statement in Go is a big improvement to how switches work in most mainstream programming languages I've used. What makes it special is that you're not creating a switch based on the value of a single variable (that typically has to be a primitive for switch to work). Instead, in Go a switch can be thought of as an if-else-if-else construct and as such, is much more versatile:

`   ``` switch {   case obj.field == 1:     // Do one thing     break   case obj.field == obj2.foo:     // Do something else     break } ```   `

Go also includes built-in support for complex numbers. This is something that will make people doing math very happy.  If the support is designed well enough, it should help all external libraries talk to each other without extra data conversion troubles. I appreciate it when a language gives strong scaffolding that helps library authors to focus on their problem and keeps them from re-inventing wheels.

The language is strongly typed but without forcing programmers to always define which type a variable is. Not only does this mean that code is shorter and more to the point, but it also allows libraries to change API without breaking code using the API. The following code will work with whatever data type the library _lib_ uses in GetFoo() and ConsumeFoo()

` ``` myFoo := lib.GetFoo() lib.ConsumeFoo(myFoo)  ``` `

Last but not least: Go functions can return any number of variables. This feature should be in all languages. Having to write tuple/triple/etc. structs or classes for every project is just irritating and should never be necessary.

## **The ugly**

The anachronisms I alluded earlier bug me somewhat. Go has chosen to go with the comfortable pattern from ancient languages like C and BASIC and has defined builtin functions like [len(), append(), etc.](http://golang.org/pkg/builtin/) in the global namespace. This is opposed to OOP style where these functions would be the responsibility of the object in question (obj.len() instead of len(obj)). By doing this, they've made sure the only cross-library compatible data types are those defined at the language level. This is a very different route from for example Java, that defines a list as an interface anyone can implement and all libraries have consolidated on these SDK interfaces. This allows programmers to use whatever list or collection implementation they want and need in a particular situation. Java of course is OOP, but we can also contrast this to JavaScript, where you can create a class that acts exactly like an Array, but is backed by a different storage mechanism, or perhaps sends notifications when modified.

Go also allows locally stored variables as well as pointers to out-of-stack variables. If you have manual memory management, locally stored values are very handy as popping the stack will free all local variables and memory management is a breeze. However, for a garbage collected language, you will never need to free memory anyways. So why have both local variables and pointers? Mixing both also makes syntax more complex and clutters code with &'s and \*'s and other curse words. I'm sure someone has an answer to this and I'd love to hear it.

The approach taken to struct (object) field visibility control is frankly weird. Instead of applying modifiers to variables or blocks of variables (think public/protect/private in Java, or public/private blocks in C++), Go uses the capitalization of the field name instead. The field "foo" would be private, but "Foo" would be public. If you choose to change the visibility of a field, you need to go through all code accessing this field. [Some may argue](http://golangtutorials.blogspot.fi/2011/06/structs-in-go-instead-of-classes-in.html) that this naming scheme helps you remember which fields are private and which are public, but this cuts both ways: If you do not remember if a field is private or public, you will be unable to write the correct field name in your code!

Classes in Go are defined by a succession of expressions: first you define a struct,then you define a constructor, then a function etc. This allows a class definition to be spread around a single or even multiple files and confusion will inevitably follow. I know that [Go isn't strictly an object oriented programming language](http://golang.org/doc/faq#Is_Go_an_object-oriented_language), but classes are nevertheless important. Maybe I'm old school, but I like the way you define the class structure and interface in a single block in a single C++ header file. Java also keeps classes nicely encapsulated, though without a separate header file Java classes do run quite long and the big picture is lost more easily.

While the syntax is mostly very familiar, Go takes some liberties with typical mainstream conventions that I find inelegant. The grouped variable definition clauses are maybe the worst offender here. While function definitions use commas to separate variables, you need to use either a semicolon or a newline (!) to separate variables. I know this is only syntax and has no big effect on the language as a whole, but why-oh-why? Can anyone explain the logic behind this? I especially dislike using whitespace as a control character.

`   ``` func foo(param1 string, param2 string) { // legal, uses commas   var (xx string, yy string) // illegal with commas   var (xx string; yy string) // legal, but weird   var (xx string yy string) // illegal, naturally. But ..   var (xx string        yy string) // .. this is legal. Whitespace inequality } ```   `

# Wrap-up

This was quite a quick look at what Go is. Admittedly I ran out of time and was only able to achieve the web scraper exercise. Once I figured the right way to use channels, the concurrency pattern in the scraper came together nicely and is at least semi-elegant. Scraping is done in a concurrent fashion while the results from the scraping are gathered and processed neatly in a single thread. The chosen pattern does have a dark side to it: it  does not allow any control over the amount of concurrency.

My views here cannot be read as deep insight into the language. Instead, they are honest first impressions of a programming language. I really like many of the concepts in Go, but found the syntax a wonky. I wouldn't say no to working with it, but at the same time I don't feel sufficiently intrigued by the language to propose it for future projects either.
