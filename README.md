# Google Summer Of Code - `xsparse`

## Overview of xsparse

`xsparse` is a library that is designed to optimize the runtime performance of sparse tensor computations. Currently, there are a lot of libraries which provide efficient storage of sparse tensors in popular formats such as COO (Coordinate format), CSR (Compressed Sparse Row), CSC (Compressed Sparse Column), DOK (Dictionary of Keys) and so on.
The main aim of `xsparse` is to generalize these formats by breaking them down into “levels” and extending their functionality such that any such tensor storage format can be constructed using these “levels”.
Our main reference is this TACO paper - [Format Abstraction for Sparse Tensor Algebra Compilers (arxiv.org)](https://arxiv.org/pdf/1804.10112.pdf)

## Goals for GSoC

The main goal for GSoC was to read and understand the code generation approaches mentioned in the paper and implement them using the compile-time features of C++20.
This also involved having a good understanding of templates in C++ and template metaprogramming, as we write instructions to generate code at compile-time.
It also gave me the opportunity to learn about the Curiously Recurring Template Pattern (CRTP) which is used in `xsparse` for defining iterators over the levels.

## Work done in Phase 1

During Phase 1, I worked on the following:

* Completed the remaining levels (two of them were already implemented) - Range, Offset, Singleton and Hashed.
* Writing the levels involved writing their respective level function definitions which define the boundaries of the iterator and also help access the coordinates.
* The hashed level was slightly different from the other three, and required more work for defining the iterator.
* I also wrote test cases for each level to ensure that it is possible to combine them and iterate properly over them.
* Additionally, some levels required implementation of `insert` and `append` capabilities which were implemented.

## Work done in Phase 2

During Phase 2, I worked on the following:

* Started off with implementing level-properties, made these properties customisable for each level.
* We decided that instead of fixing the containers that were used, such as `std::vector`, `std::map` and `std::set`, it should be made flexible so that containers with desirable properties can be used, if required. This required container_traits to be implemented.
* Started working on the lengthiest part of the project, co-iteration. Co-iteration required figuring out how to iterate simultaneously over 'n' levels in order to merge and carry out operations between these levels. This was the most challenging part for me.
* Finally completed co-iteration and ironed out bugs with the help of my mentor. Wrote tests and got the final PR merged.

## List of Pull Requests

1. [Implemented range and offset levels](https://github.com/hameerabbasi/xsparse/pull/4)
2. [added singleton level + COO test](https://github.com/hameerabbasi/xsparse/pull/5)
3. [added hashed level + tests](https://github.com/hameerabbasi/xsparse/pull/6)
4. [CI pass fix](https://github.com/hameerabbasi/xsparse/pull/8)
5. [Add Append Capability to Compressed Level + Test](https://github.com/hameerabbasi/xsparse/pull/9)
6. [Add Level properties](https://github.com/hameerabbasi/xsparse/pull/10)
7. [Add Level Properties + Container Traits](https://github.com/hameerabbasi/xsparse/pull/11)
8. [Add Level Properties](https://github.com/hameerabbasi/xsparse/pull/12)
9. [Add iterator merge](https://github.com/hameerabbasi/xsparse/pull/13)

## Next steps

There is some work still left to be done in `xsparse` before it can serve as an end-to-end library for sparse tensore computations. We need to implement the high-level code generation algorithm and find a way to efficiently carry out operations between different level combinations.

We also plan on writing a `cppyy` wrapper for calling C++ code from Python and vice-versa.
I plan to coordinate with my mentor whenever possible post-GSoC and accomplish these objectives.

## Acknowledgements

I had a really great time this summer working on building `xsparse`. I would like to thank Python Software Foundation, SciPy and Google Summer of Code for this wonderful learning opportunity.

I would like to thank my mentor, [Hameer Abbasi](https://github.com/hameerabbasi) for always being there to answer all my questions, even the silliest of them! The amount of things I've learnt from my mentor in this short period of time is invaluable, to say the least.

The best part about GSoC is that every step is a challenge, and how you learn to overcome these challenges with the help of amazing people!

## Follow `xsparse`

You can follow the work done on `xsparse` here : https://github.com/hameerabbasi/xsparse
