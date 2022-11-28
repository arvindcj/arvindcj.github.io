---
layout: post
title:  "Metaprogramming Ruby"
date:   2022-11-15 14:41:39 +0530
updated: 2022-11-17 14:41:39 +0530
categories: software_engineering
---

## Introduction ##

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
  puts Hello.new.world

  Output# Hello! World
```

Notice that a Sting is transformed into a new Class "Hello" containing the method "world". Which brings us to the question, what does `eval` do? is it a hook into the compiler? If 'Yes' will it produce the same output when executed on a Ruby compiler?

Although, as powerful as `eval` is, the idea of a program looking into itself seems more intriguing.

## Reflection API ##

It is a feature of a programming language to examine and modify its structural components during program execution. Ruby achieves this feat through methods implemented in the Kernel, Class and Module.  

|   | Module  | Class  | Method  | Variables | Blocks |
|---|---|---|---|---|---|
| **Create** |   |   |   |  |   |
| **Read** | ancestors<sup>k</sup> | ancestors<sup>k</sup> |   |   |   |
|  |   | class |   |  |   |  
|  |   | superclass |   |  |   |                 
| **Update** |   |   |   |  |   |
| **Delete** |   |   |   |  |   |

|  |   |   |   |  |   |
```
Key

k - Kernel method

```

## Conclusion ##
