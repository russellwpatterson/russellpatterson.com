---
author: "Russell Patterson"
date: 2014-03-13 05:14:30+00:00
draft: false
title: 'Pattern of the Week: Prototype'
url: /2014/03/pattern-of-the-week-prototype/
categories:
- Pattern of the Week
- Technical
---

_This is the seventh in a series of "Pattern of the Week" posts. I'm primarily sticking with the [Gang of Four](http://www.amazon.com/gp/product/B000SEIBB8/ref=as_li_qf_sp_asin_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B000SEIBB8&linkCode=as2&tag=russepatte-20) patterns, but I may branch off occasionally. Thanks for reading._

Type: **Creational**

This week's pattern is called the Prototype pattern. This pattern is used when you need to create exact copies of objects. Let's look at our example Prototype class:
 

    
    public class StreetSign
    {
        public StreetSign(string shape, string text)
        {
            Shape = shape;
            Text = text;
        }
    
        public string Text { get; private set; }
        public string Shape { get; private set; }
    
        public StreetSign Clone()
        {
            return new StreetSign(Shape, Text);
        }
    }



This StreetSign class has two properties - Text and Shape, and a method called Clone. The prototype pattern is fully represented by the "Clone" method. Basically, the Clone method should be implemented so that it returns an exact copy of the object on which it is called. 

There are many ways to implement this pattern. A most ideal way would be if you could have the method [reflect](http://en.wikipedia.org/wiki/Reflection_(computer_programming)) over the entire object. This would mean that you could add properties to the class without having to change the Clone method. The simplest way is the way that I implemented it in the code sample. A new instance is created and the properties are set on the new object (in this case, via the constructor). Either way is valid.

It should also be noted that there is a method on System.Object in .NET called MemberwiseClone, which essentially implements the Prototype pattern. The only thing about this method is that it creates a shallow copy, so if you have objects within your objects, those won't be copied. Instead, the same instances of those sub-objects will be referenced by the clones.

This is pretty much all there is to this pattern. If you need additional help, please take a look at the full source code below, or feel free to comment, and I'll respond directly.

Visit next week for an explanation of another pattern.

[View Sample Code](https://github.com/russellwpatterson/pattern-of-the-week/)
