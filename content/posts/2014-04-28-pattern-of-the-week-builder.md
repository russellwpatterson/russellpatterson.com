---
author: "Russell Patterson"
date: 2014-04-28 04:01:57+00:00
draft: false
title: 'Pattern of the Week: Builder'
url: /2014/04/pattern-of-the-week-builder/
categories:
- Pattern of the Week
- Technical
---

_This post is part of a series of "Pattern of the Week" posts. I'm primarily sticking with the [Gang of Four](http://www.amazon.com/gp/product/B000SEIBB8/ref=as_li_qf_sp_asin_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B000SEIBB8&linkCode=as2&tag=russepatte-20) patterns, but I may branch off occasionally. Thanks for reading._

Type: **Creational**

This week's pattern is called the Builder pattern. The builder pattern is a common way to create an object, using methods and properties to set up exactly the kind of object you want, then calling a Build() method to actually create the object. Let's look at an interface for a builder object:
 

    
    
    public interface IShirtBuilder
    {
        Color ShirtColor { get; set; }
        int ShirtSize { get; set; }
        ShirtBuilder.IShirt Build();
    }



This interface has a couple properties, ShirtColor and ShirtSize, and a method called Build. Let's look at ShirtBuilder, the concrete implementation of this interface:
 

    
    
    public class ShirtBuilder : IShirtBuilder
    {
        public ShirtBuilder()
        {
            this.ShirtColor = Color.Black;
            this.ShirtSize = 1;
        }
    
        public Color ShirtColor { get; set; }
        public int ShirtSize { get; set; }
    
        public IShirt Build()
        {
            // We could create any type here that implements IShirt.
            var shirt = new Shirt();
            shirt.Color = this.ShirtColor;
            shirt.Size = this.ShirtSize;
    
            return shirt;
        }
    }
    



This class creates a Shirt object, which implements the IShirt interface. This interface and class are incredibly simple, so we don't need to go over them here. Please look at the source code if you're curious.

Now that we have the builder ready to create shirts, what do we need to do now? Let's use it! A builder is also really easy to use.
 

    
    
    var builder = new ShirtBuilder();
    
    builder.ShirtColor = Color.Blue;
    builder.ShirtSize = 45;
    
    var shirt = builder.Build();
    



The shirt variable above now has a fully initialized Shirt object with all of the parameters that you wanted. It's ready to use.

The question is: when should I use this? You should use this pattern when you need to specify a lot of details about the object you're creating. If you just need an object, with maybe one or two properties that need initialized, you should consider using the [Abstract Factory](http://russellpatterson.com/2014/02/pattern-of-the-week-5-abstract-factory/) pattern or a simple copy constructor instead. If there are a ton of things that you need to set on the object, Builder is the way to go.

This is pretty much all there is to this pattern. If you need additional help, please take a look at the full source code below, or feel free to comment, and I'll respond directly.

Visit next week for an explanation of another pattern.

[View Sample Code](https://github.com/russellwpatterson/pattern-of-the-week/)
