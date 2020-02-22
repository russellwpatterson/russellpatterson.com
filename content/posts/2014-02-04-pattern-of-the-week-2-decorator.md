---
author: "Russell Patterson"
date: 2014-02-04 02:13:46+00:00
draft: false
title: 'Pattern of the Week: Decorator'
url: /2014/02/pattern-of-the-week-decorator/
categories:
- Pattern of the Week
- Technical
---

_This is the second in a (hopefully) long series of "Pattern of the Week" posts. I'm primarily sticking with the [Gang of Four](http://www.amazon.com/gp/product/B000SEIBB8/ref=as_li_qf_sp_asin_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B000SEIBB8&linkCode=as2&tag=russepatte-20) patterns, but I may branch off occasionally. Thanks for reading._

Type: **Structural**  
Difficulty: **Beginner**

This week's "Pattern of the Week" is the Decorator pattern. To explain this pattern, I'm going to start with an explanation of the [Open/Closed Principle](http://en.wikipedia.org/wiki/Open/closed_principle). The Open/Closed Principle is one of the five "[SOLID](http://en.wikipedia.org/wiki/SOLID_(object-oriented_design))" principles outlined by Robert C. Martin in his works. The principle states that a class should be open for extension, but closed for modification. What does this mean? It's actually pretty simple. We shouldn't change the behavior of a class after it has been defined, and we should be able to extend the class by various means to add functionality. One of the ways to extend a class without modifying it is the Decorator pattern. Without further ado, here's a class:
 

    
    public class Person : IPerson
    {
        public string FirstName { get; set; }
        public string LastName { get; set; }
    
        public string GetFullName()
        {
            return FirstName + " " + LastName;
        }
    }



Well, that's a pretty simple class. It implements the following interface:


    
    public interface IPerson
    {
        string FirstName { get; set; }
        string LastName { get; set; }
        string GetFullName();
    }



Nothing revolutionary there. We've represented a pretty basic person. So, let's say we want to print out the information on the console. Here's one way to do it:


    
    
    var p = new Person();
    p.FirstName = "John";
    p.LastName = "Public";
    
    var fullName = p.GetFullName();
    Console.WriteLine("Person: {0}", fullName);
    



Since this only deals with the Person class, maybe we should add it to the Person class, as a Print method. But wait, wouldn't that be modifying the class to extend it? Yes. So, we shouldn't do that. Worse, it would also be violating another SOLID principle: The [Single Responsibility Principle](http://en.wikipedia.org/wiki/Single_responsibility_principle). This class would have the responsibility to keep Person information, as well as the responsibility to print it out to the console. Well, we don't want to break two SOLID principles, so let's try something using the Decorator pattern instead. We'll create the following class:


    
    public class PrintablePerson : IPerson
    {
        private readonly IPerson _person;
        public PrintablePerson(IPerson p)
        {
            _person = p;
        }
    
        public string FirstName
        {
            get { return _person.FirstName; }
            set { _person.FirstName = value; }
        }
    
        public string LastName
        {
            get { return _person.LastName; }
            set { _person.LastName = value; }
        }
    
        public string GetFullName()
        {
            return _person.GetFullName();
        }
    
        public void Print()
        {
            Console.WriteLine("Person: {0}", this.GetFullName());
        }
    }



Now, there are a couple of important notes about the PrintablePerson class. First of all, you'll notice that it implements the same interface as the Person class. It also adds a method called Print. Finally, it takes _any_ implementation of IPerson in the constructor, then hands off all calls to IPerson properties and methods to that class. So, how does this help us?

Well, we can now add printing functionality to _any_ IPerson implementation, without changing the class itself. This new class also has only one responsibility: printing. That covers both the Single Responsibility Principle and the Open/Closed Principle. So, let's look at this in action:


    
    var pp = new PrintablePerson(new Person());
    
    pp.FirstName = "John";
    pp.LastName = "Public";
    
    pp.Print();
    



By decorating the Person class in the above code, we were able to extend the class, without actually modifying the original class. This is incredibly powerful. By using this technique, you can keep your classes simple, and make sure that they only have one responsibility. You can also avoid changing the code in a class that you know is working, so you don't have to worry as much about introducing bugs. (You should still test though!)

You may be asking yourself, "that's good and all, but when do I use it?" Well, there are countless ways to use the pattern. Microsoft actually uses the pattern fairly heavily in the .NET Framework, mainly with the System.IO classes. You could use it to add logging to a class that doesn't have it built in. You could use it to handle exceptions from a class that doesn't handle them. Again, the possibilities are nearly endless.

That’s all! Visit next week for an explanation of the Strategy pattern.

[View Sample Code](https://github.com/rwpcpe/pattern-of-the-week/)
