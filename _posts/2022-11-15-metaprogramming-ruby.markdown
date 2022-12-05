---
layout: post
title:  "Metaprogramming Ruby"
date:   2022-11-15
updated: 2022-12-05
categories: software_engineering
---

## Introduction ##

I had begun my programming career in languages like Java, C and C++, but had not come across the idea of Metaprogramming. I heard about this technique working on a project that required me to program in Ruby. I remember trying to understand this new language and its funky syntax in terms of what was familiar. Learning through analogy made it was easy to understand the bits that were syntactically similar, but this approach had a converse effect when faced with novelty. This time around my approach is ab initio from fundamentals. This article is a gentle introduction to Metaprogramming in the Ruby context. I will introduce the concept with a simple example, a cheat sheet and finally end with an example on metalinguistic abstraction.

Metaprogramming is essentially programming language features that enable programmers to "create programs that write programs". In-other terms the ability of a program to modify itself at runtime without the need for recompilation. The Ruby Kernel method `eval`  accepts a `String` and evaluates its argument within the context of the main program.

I had been programming for a while in languages like Java, C, and C++, but had yet to come across the idea of Metaprogramming. But then a project required that I program in Ruby and RSpec grabbed my attention. I remember trying to understand this new language and its funky syntax in terms of what was familiar. Learning through analogy made it easy to understand the bits that are syntactically similar, but had the converse effect on the differences. This time around my approach is to understand the subject from its fundamentals. This article is a gentle introduction to Metaprogramming in the Ruby context. I will introduce the concept with a simple example, a cheat sheet, and finally, end with an example of metalinguistic abstraction.

Metaprogramming is essentially programming language features that enable programmers to “create programs that write programs”. In-other terms the ability of a program to modify itself at runtime without the need for recompilation. The Ruby Kernel method `eval` accepts a `String` and evaluates its argument within the context of the main program.

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

Although, as powerful as `eval` is, the idea of a program looking at itself seems more intriguing.

## Reflection API ##

It is a feature of a programming language to examine and modify its structural components during program execution.

|   | BasicObject  | Object | Kernel | Module | Class |
|---|---|---|---|---|---|
| **Create** |   | define_singleton_method  |   |  |   |
|  |   | clone  |   |  |   |
|  |   | dup |   |  |   |
|  |   | instance_variable_set  |   |  |   |

| **Read** | `__id__` | ancestors |   |   |   |
|  |   | class |   |  |   |  
|  |   | superclass |   |  |   |  
|  |   | inspect  |   |  |   |
|  |   | instance_of?  |   |  |   |             
| **Update** | singleton_method_undefined  |   |   |  |   |
| **Delete** | singleton_method_removed |   |   |  |   |
| **eval** | `__send__` |   |   |  |   |
|  |  instance_eval |   |   |  |   |
|  | instance_exec |   |   |  |   |


## Metalinguistic Abstraction ##

One of the key uses of Metaprogramming is its utility in implementing Domain Specific Languages (DSL) or Metalinguistic Abstraction.

Software Engineering like other engineering disciplines deals with complexity by decomposing large systems into simpler and more fundamental units. Therefore, larger software systems are built using language primitives called atoms in a layered approach. Each layer serves as a base for the layer above, finally exposing the user interface. Users interacting with this final layer rarely see the complexity of the underlying system enforced by the idea of abstraction.

It is often desirable to have features in a programming language to extend itself to meet the requirement of a domain called Domain Specific Languages (DSL).

RSpec Example,

```
  describe :testing_group do  # Test Group
    it :test01 do             # Tests
    end

    it :test02 do
    end
  end

```   

It can be seen that `describe` and `it` look like language constructs (keywords), but are methods defined in the RSpec DSL.


## Conclusion ##

This article was designed to be very brief, integrating a cheat sheet with simple examples to demonstrate the basic ideas. However, It will serve as a foundational unit for exploring other ideas.

Please be aware that all material presented in my articles is subject to change. The source of these changes is through feedback and restructuring ideas.
