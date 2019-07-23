---
title: Is a completely universal programming language possible at all?
permalink: /cupl/
---

Quite a lot of time has passed since the emergence of first programming languages.  Outstanding minds of the last century came up with brilliant ideas that were implemented in various programming languages: lambda calculus, formal grammars, static typing, structural programming, composite types, modularity, abstract types,  etc ... 

It looks like a long time ago it would be possible to create a completely universal programming language suitable for all. At the same time, we see that none of the existing programming languages could be considered as completely universal. 

But wait, let's define what does mean term "completely universal programming language". By the term, I mean a language that could be most efficiently used in various fields of human activity with the most efficiency.

So why I am sure that none of the existing programming languages could be considered as completely universal? It is caused by the fact that each modern language is being specialized in some particular field of business. And the requirements between different fields are very different. 

For example to quickly make a prototype a developer need something lightweight and smart. Easy to start with, easy to configure. It is not obliged to be fast. On the other side to make software for a controller a developer needs the generated code to be as fast as possible and cannot afford automatic manager of memory because of small memory footprint requirements. But again a theorem-proof assistant requires lambda calculus based implementation which requires in its turn automatic memory manager. So on and so on.

Now thoughtful reader would ask: ok but why do we need a completely universal programming language at all? 
Well, having different languages for different purposes lead to those problems: 
1. Bridges between languages don't allow seamless communication between components implemented in different languages. 
2. Build walls between developers. And syntax here is a minor one. It could be learned very quickly. But the worst thing is that each language has its pitfalls (complicated opaque specifics). And quite often those pitfalls are very tricky. Therefore it requires a lot of time to bring the level of using a programming language to the professional one. For example, a developer switching to a new language may feel safe writing some code in a new language because in the old one the same kind of code was safe but in the new one it would lead to a subtle bug. 
3. The necessity to implement different universal algorithms again and again and again in different languages (sorting, search, collections, etc ... ). It is useless wasting of developers time thus slowing down humanity advance. 

Now when we have agreed that we have problems because of a completely universal language absence we need to think about how could look the language. 

I think it is clear that those requirements for different languages are quite controversial to each other. Some business requires enough durable technologies, maybe even mathematical prove, someone can't afford and don't need too expensive and complex technologies. Some startups need something very easy to use and smart to quickly build a prototype. 

Looks like that to make a completely universal language we need to connect somehow concise syntax and easiness to understand code, clear non-verbose code and best performance of a generated application, ability to quickly prototype and static code checking, small memory footprint and automatic or at least automated memory control, etc.

I think it is clear that we can't have everything at the same time. 

For example, Rust provides automated memory control. But it does so at the price of adding memory control to the type system. Haskell separates pure functions from other ones at the price of adding IO monads to the type system. All this complicates development process and also those languages have a steep learning curve.

Speaking about performance, mostly all modern languages have some features needed to do performance optimization only but opening doors for some subtle bugs. Example: different integer types and related integer overflow bugs. And there are a lot of features which are being used to tune performance only but make everything more complicated increasing possibility of introducing a bug. I believe that those performances-only related constructions are obvious violations of abstraction principles. We mix a pure algorithm and particular computer-specific implementation details. 

And now I would like to discuss the 3rd tradeoff. Compilers of all modern languages have to be fast enough. And because of that, they can provide neither maximum theoretically possible performance optimization nor durability levels. 

So let's talk first about static type system. There a lot of statements about programming by contract. Nearly every modern type system allows expressing some aspects of contracts. But there are no technical means to express those contracts at all. Using abstract classes, interfaces, traits, etc to express a contract we just express some vague verbs or nouns without any constraints about them. Every contract is implicitly assumed but there is no means to be sure that every implementation correctly implements the contract. As an example let's consider Haskell's monad typeclass. A monad has to obey 3 laws. But there is no means in Haskell to prove that an instance of the monad typeclass follows the 3 monadic laws. So on and so on.

The situation about performance is mostly the same. Some time ago I did a small experiment. You can read about it here https://jinnzest.github.io/csote. It appeared that applying only computer architecture-specific optimizations (bug keeping the same algorithm thus keeping the same algorithmic complexity) we can boost an application to be 500 times faster. Now is it much or not? Consider a mobile device which is widespread nowadays. 500 times faster means 500 times longer the battery life-time. In its turn, it means 500 less poisonous batteries which have to be recycled.  We don't allow a compiler to waste too much time of a developer but then we waste millions of hours of end-users mobile devices. Consequently, we produce much more poisonous garbage than we could. 

My conclusion is the complexity and unreliability of modern software arises from mixing into one single mess unrelated things (Mixing of computer-related optimizations and means to express a contract). I believe that separating those unrelated concepts would allow us to create a completely universal programming language. But this separation doesn't mean that we should give one thing in favor of another one. We observe in that case broken abstraction principle. Applying the principle we decompose a complex object to simpler pieces and analyze each of them separately but then we don't have to throw away some of them. Applying abstraction principle to programming we are dealing with complexity by moving pieces of code to modules, classes, instances of typelcasses,  methods, functions, etc.  But we don't throw away some pieces of needed code just because it is too complex to understand it altogether.

My conclusion is the complexity and unreliability of modern software arises from mixing into one single mess unrelated things (Mixing of computer-related optimizations and means to express a contract). I believe that separating those unrelated concepts would allow us to create a completely universal programming language. But this separation doesn't mean that we should give one thing in favor of another one. We observe in that case broken abstraction principle. Applying the principle we decompose a complex object to simpler pieces and analyze each of them separately but then we don't have to throw away some of them. Applying abstraction principle to programming we are dealing with complexity by moving pieces of code to modules, classes, instances of typelcasses,  methods, functions, etc.  But we don't throw away some pieces of needed code just because it is too complex to understand it altogether. So we just need to apply the abstraction principle while designing a programming language the same way as we do while developing some software application. 
