---
layout: post
title:  "Metaprogramming Ruby"
date:   2022-11-15 14:41:39 +0530
updated: 2022-11-17 14:41:39 +0530
categories: software_engineering
---

## Introduction ##

I had been programming for a while in languages like Java, C and C++, but had yet to come across the idea of Metaprogramming. But then a project required that I program in Ruby and RSpec grabbed my attention. I remember trying to understand this new langage and its funky syntax in terms of what was familiar. Learning through analegy made it was easy to understand the bits that are syntaxtually similar, but had the converse effect on the differences. This time around my approach is to understand the subject from its fundamentals. This article is a gentle introduction to Metaprogramming in the Ruby context. I will introduce the concept with a simple example, a cheat sheet and finally end with an example on metalinguistic abstraction.

Metaprogramming is essentially programming language features that enable programmers to "create programs that write programs". In-other terms the ability of a program to modify itself at runtime without the need for recompilation. The Ruby Kernel method `eval`  accepts a `String` and evaluates its argument within the context of the main program.

```
  File: metaprogramming.rb

  a = "World"
  eval("puts 'Hello! #{a}' ")

  Output# Hello! World
```

The sub-program could also be:

```
  File: metaprogramming.rb

  a = "class Hello; def world; \"Hello! World\"; end; end;"
  eval(" #{a}")
  puts Hello.new.world  # String -> Class Hello containing Method world.

  Output# Hello! World
```
**Questions to think about:**

1. what does `eval` do?
2. Is it a method hook into the Ruby compiler?
3. If indeed a compiler hook will it produce the same output when executed on a Ruby compiler?
4. The two examples from above differ in the construction of its sub-program. The second creates a Ruby class, while the first does not. Therefore, is the first program an example of Metaprogramming?

Although, as powerful as `eval` is, the idea of a program looking onto itself seems more intriguing.

## Reflection API ##

It is a feature of a programming language to examine and modify its structural components during program execution. Ruby achieves this feat through methods implemented in the Kernel, Object and Module.  

|   | BasicObject  | Object | Kernel | Module | Class |
|---|---|---|---|---|---|
| **Create** |   |   |   |  |   |
| **Read** | ancestors| ancestors |   |   |   |
|  |   | class |   |  |   |  
|  |   | superclass |   |  |   |                 
| **Update** |   |   |   |  |   |
| **Delete** |   |   |   |  |   |

|  |   |   |   |  |   |

## Metalinguistic Abstraction ##

One of the key uses of Metaprogramming is its utility in implementing Domain Specific Languages (DSL) or Metalinguistic Abstraction. Most of Software Engineering is the process of delaing with complexity theough combining primitives to form more complex forms through abstraction.

  


## Conclusion ##

This article was designed to be very brief incprorating the idea of a cheatsheet with a simple example to demionstrate the basic idea. It will serve as a starting point for ideas to come.    
