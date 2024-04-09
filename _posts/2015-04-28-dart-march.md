---
title: "Dart - March"
date: "2015-04-28"
categories: 
  - "one-language-per-month"
background: "/images/olpm-dart.png"
layout: post
---

I attended the Goto conference 2011 in Amsterdam where Kasper Lund, the creator of Dart, officially announced Dart. The features of the language grabbed me immediately but during that time it was not mature enough to use in real projects and I never remembered to check back on how the language was doing.

![dart-logo-wordmark.png](/images/dart-logo-wordmark.png)

At least from my perspective, Dart and JavaScript have a lot in common. Both are used for mainly two things: browser side and server side request-response or event processing. For this reason I will be comparing these two even though the languages have many deep rooted differences.

JavaScript is missing concurrency. If you've read my earlier rants on different languages, you will know that concurrency is something that I rank highly in programming languages. Asynchronous calls alleviate much of the need for concurrency, but it is still leads to a dead end: you cannot use JavaScript if you need concurrent processes. There are ways around this of course, but they require hacks, additional constraints and extra effort that really would be better spent on the problem you are actually solving. Dart uses the concept of isolates to deal with concurrency. Basically these are like threads, each running their own event loop (for asynchronous calls) without any shared memory. The isolates communicate with each other through messaging. It is an interesting middle ground allowing concurrency in a safe manner without the complexity of classical low level mutual exclusion mechanisms. It might however prove to be a resource hungry pattern for the Dart runtime or compiler to implement.

Another main grievance with JavaScript I have is the lack of typing. Not having types makes programming very fluid and fast; libraries are simple to integrate, and options can be easily transmitted as anonymous objects. The downside to this freedom is confusion brought up when refactoring, upgrading or changing libraries, or reading old code. The depth of this confusion ranges from is very simple issues to huge headaches when you have tens or hundreds of thousands of lines of intricately weaved code. Having declared types will not automatically fix your code, but the constraints types set allow for tools to immediately point to problematic parts of your code. Dart supports typing and what's even better: they're optional.

Another pet peeve of mine in JavaScript is the lack of a well defined class. The newest version of JavaScript, ES6, will finally have classes, but we're still waiting for that to be finalized and rolled out. Dart gives programmers a formal OOP model with clear inheritance and also goodies like an innovative model for [getters and setters](https://www.dartlang.org/docs/dart-up-and-running/ch02.html#getters-and-setters).

Dart also benefits from having futures instead of callbacks from the ground up. This does not disallow using a callback model, but it does encourage library developers to use the much superior future (or "promise" depending on what you call them) model.

Dart still inspires me as a language - I really need to find a project I can test it on.
