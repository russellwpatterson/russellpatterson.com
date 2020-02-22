---
author: "Russell Patterson"
date: 2016-10-31 02:19:18+00:00
draft: false
title: Hello, Ruby!
url: /2016/10/hello-ruby/
categories:
- Ruby
---

As part of my professional development plans for the year, I'm learning the Ruby language and the Ruby on Rails framework. Now, I'm just getting started so I'm a complete newbie, but here's the first program that we all write when we're learning a language: Hello, world!

I'm using the "irb" REPL command instead of actually saving source file(s) at this point. Here's how I started:


    
    def hello_world
      puts "Hello, world!"
    end
    
    hello_world



**Output:** _Hello, world!_

Basic, right? Now, let's take some user input, and say hello to an entered name.
 

    
    def hello(name)
      puts "Hello, " + name + "!"
    end
    
    name = gets.chomp
    
    hello(name)



**Input:** _Russell_
**Output:** _Hello, Russell!_

If you just use gets, you will also receive the newline character on the input. The chomp function removes this character.

That's all for now. I'll be creating more posts as I continue learning Ruby.

