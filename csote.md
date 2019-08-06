---
title: Computer specific optimization techniques experiment
permalink: /csote/
---

The experiment had as its object next targets:
1. Compare the performance difference between the same application implemented in Scala and Rust programming languages. 
2. Research how different computer specific optimizations could boost the performance of the application. 

In the research, no optimizations related to algorithmic complexity were applied. At all. All optimizations were only about some computer architecture related things like internal CPU memory cache, compressing few objects into the smallest piece of computer memory, etc.

A genetic algorithm implementation was chosen as the target of optimizations because it intensively uses memory. The distinguishing feature of this algorithm is that each time it can find a solution to a problem at a different time. Moreover, it can search for the most optimal solution indefinitely. It only guarantees that it can find quickly enough one of the most optimal solutions.  

Consequently, in order for the measurements between runs to be identical, I modified it a little bit so instead of using randoms on each genetical operation I used monotonically increasing number generators for each call. Therefore I was able to write integration tests which run each time with the same result (so after each optimization I was sure that algorithm was still the same). But even most important for the research was that benchmarks always run practically the same amount of time per run. Thanks to it I was able to measure performance boost pretty accurately after each optimization. 

You can see each applied optimization step in those repositories: https://github.com/jinnzest/genetic-algorithm-scala,
https://github.com/jinnzest/genetic-algorithm-rust. 

In each step one kind of optimization is being applied in each implementation, performance measured and written to commit message. I used absolutely the same algorithm for both versions. Started from a rather functional approach (immutability everywhere, pattern matching, etc) and then step by step went to more imperative style (reusing all memory places for new objects instead of allocating new memory for each one, decomposing objects to bits, etc). 

Results: 
1. Rust allowed to speed it up about 30-40 % more than Scala. But more important is that Rust version at the end was mostly the same readable and concise while Scala version code size bloated about 2 times and got very complicated.  Rust version got bigger only about 35% and code stayed clear and easy to understand. Also, it appeared that it was not possible to boost the Scala version more than 100 times without introducing pools of objects (the optimization reduced GC load). Without it, all other optimizations didn't increase performance. 

2. 500 times speed boost means that there is a lot of work compilers could do but don't. Those tricks are not very smart so a compiler could do them itself. And 500 times it not 2 or 3 times. It is too much. 
