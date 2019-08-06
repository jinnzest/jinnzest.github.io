---
title: "Design of programming languages: must we always do trade-offs?"
permalink: /dpl/
---

Each of modern programming languages emphasizes some subset of aspects while completely abstracting away other ones. For example, Haskell allows explicitly expressing side effects at the level of its type system but abstract away memory. Rust at the level of type system allows controlling memory but abstract away side effects. Also, there are languages which prioritize simple to learn semantic but abstract away performance, correctness, etc.  

In each case, language designers accentuate a few concepts while completely ignoring everything else. Ok, abstraction is a very powerful and useful mechanism. It allows us to abstract away minor details to simplify analysis. But in a case when some object consists of some amount of important for us aspects then we just can't deal with one of them and ignore other ones. 

Consider for example a car. Imagine that a designer was concentrating on only one aspect during designing a car. For example, if a designer was considering a car from point of view of speed maximization we would get something able to outrun a jet. It would have a minor defect though: the absence of breaks. Also the absence of all other safety means. Or a designer could abstract away everything but safety. The car would be very safe but drive slower than a bicycle. Then came an old-school designer and said that everything mentioned above doesn't matter and only the speed of constructing a car does matter. You can imagine the quality of the resulting car.

I think it is obvious that in case of a car designing we can't abstract away any of its major aspects. Like engine power, fuel consumption, safety, comfort, design. To deal with complexity we are working out each aspect separately but we DON'T give up one of them in favor of other ones.

That is why I believe that a programming language should be designed the same way. Such that when we develop software we use something like iterations over abstractions. We analyze the first aspect of a piece of code abstracting away others, then the second one abstracting away everything else, etc. As a result, we will have software with complex aspects which would be very difficult to deal with at once.

Unfortunately, modern programming languages don't allow us to deal with software complexity. Don't allow us to work it out step by step abstracting away all other steps except the current one. We have to keep in mind tons of things at the same time: the size of each integer type, considering all corner cases of input data, resources acquiring/releasing, algorithmic complexity of code,  memory consumption complexity,  the implicit influence of one component to another one, domain of functions,  etc, etc. Not surprising why modern software is so complicated and contains so many bugs. 

But if a language, on the contrary, provides means to split code into separate aspects we will have to examine only one of them at once abstracting away all other. Thus mental load will be decreased and also we will be able to design more powerful and expressive language constructions to define each aspect.  It will allow us to create more durable, fast and easy to understand software than allows us any of existing languages.  

