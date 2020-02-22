---
author: "Russell Patterson"
date: 2013-06-16 21:41:50+00:00
draft: false
title: 'Team Foundation Service: How do I delete a Team Project?'

url: /2013/06/team-foundation-service-how-do-i-delete-a-team-project/
categories:
- Team Foundation Service
---

I came across this problem earlier today, and I realized that it isn't clear how to delete a team project. It is, however, really easy.

All you have to do is open the "Developer Command Prompt for VS2012" (located in Start > All Programs > Microsoft Visual Studio 2012 > Visual Studio Tools) and type the following command (assuming you have the server mapped in Visual Studio).

`TfsDeleteProject /force /collection:https://ID.visualstudio.com/DefaultCollection PROJECT`

Replacing the word "ID" with whatever your TFS Online ID is, and "PROJECT" with the name of the team project that you wish to delete.
