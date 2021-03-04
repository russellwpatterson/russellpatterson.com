---
author: "Russell Patterson"
date: 2020-02-22 20:00:00+00:00
draft: false
title: 'Site Updates'
url: /2020/02/site-updates/
categories:
- General
---

I wanted to spend a few minutes and update anyone out there listening on what I'm working on and how things are progressing in my life.

First of all, a couple status updates on some things that I've been saying are "coming soon" for about 10 years now:

* **Alarm 4.0**

   I've made a number of false starts to get the features I want in Alarm 4 developed and released to the community. At one point, I know there were over 30k downloads of Alarm 3.5, and something like 1500 active daily users. I was blown away all those years ago by the impact my dumb little spare time project had on so many people. I still get emails occasionally of people who tell me how much they love it and how cool it would be if I'd continue developing it, or if I'd open source it.

   Honestly, I've spent the last 10 years wanting to work on Alarm 4, but I've been unable to motivate myself for more than a couple of days. Sadly, I just don't think I was interested in the project any more.

   One of the things that I do want to do is update it to run on .NET Core 3. I think this will likely be a minor revision, not a 4.x version. More than likely it'll be v3.9 or something like that.

   If I do get the time and focus to re-platform it onto .NET Core, I will be willing to open source it. The shame in me won't let me release code that I started working on when I had -2 years of professional experience, but giving the codebase a once over with some re-architecting will make it "community ready".

* **Simple Lookups 3**

   When I wrote Simple Lookups, it was something that I was planning to use at the company that I worked for at the time. I spent only about 8 months actually developing it, and as part of that, I got a chance to create a useful NuGet package, and even made an appearance on a podcast to talk about it.

   Simple Lookups has been downloaded a couple thousand times, which is awesome, but more modern solutions like Entity Framework are far more popular and perform just as well. Because of this, I haven't made any changes to that codebase since 2016. I've thought more than once that I should actually get it working on the .NET Core platform, but I've never got around to it. But, over the next six months, I plan to create a new version of Simple Lookups that will run on the .NET Core platform. It will still be limited to SQL Server lookups, but I will make sure that the codebase is compatible with .NET Standard and runs well on both Core and Framework.

* **Pattern of the Week**

   I still want to do these, but I got burnt out. I'm thinking about rebranding as "Pattern in Focus" or something like that, and shoot for trying to get one out every couple weeks.

* **Simple Settings**

   I had started a project based on some of the work I had done on Alarm 4 - a really simple way to manage application settings. Basically, this library would handle all the storage of key-value pairs into either the Windows Registry, INI files, XML files, or JSON files.

   I made it about 50% through the development of a 1.0 version, but then I shelved it. I'm not sure that this will ever be released, and in fact, I'm only mentioning it so that I don't forget about it.

* **Chron**

   I've worked a little bit on a simple git tagging tool that automatically increments and pushes a git tag to the remote. It's pretty heavily based on a solution we had at one of my clients, but I'm writing it from the ground up in C#. I'm thinking it'll be a few months on this one before I'm ready to release it.

* **RussellWritesCode.com**

   I've spent a bit of time over the last couple weeks to bring over all of my previous content from my old blog into this format. I believe things came over, but there's always a chance it didn't. If you see something, say something.

As far as general life updates, we now have three cats - Avery (8), Polly (8), and Daisy (1). I'm going to have to do a better job of posting about them, or at the very least, start throwing some things on Instagram.

