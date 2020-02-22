---
author: "Russell Patterson"
date: 2009-09-03 04:00:52+00:00
draft: false
title: MP3 Decoder/Player
url: /2009/09/mp3-decoderplayer/
categories:
- Technical
---

Today, I’m starting to look at the MP3 specification in order to write an unmanaged C++ library which will hopefully be able to read, decode, and play all MP3 files. This code will be integrated with my Alarm clock software eventually, but for now I just want to get it working. This will be my major project for the next few months which means that after the planned Alarm updates, I will not be touching it for a little while.

A few things I need to consider:
- Different versions of the MP3 standard.
- DIfferent versions of the ID3 tagging standard. (1.0, 1.1, 2.0, 2.2, 2.3, 2.4, etc)
- MP3’s encoded with WinAMP fail to pass the standard. iTunes might as well.
- Speed. I cant have a slow decoder. I need to use native code and use the most efficient data structures available.
- Do I want to make this open source?

I might try to find another open-source decoder and build off of it, but I’m not sure yet.
