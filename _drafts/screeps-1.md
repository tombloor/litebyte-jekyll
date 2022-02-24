---
layout: post
title:  "Screeps 1 - Introduction"
date:   2022-02-11 09:00:00 -0500
categories: Programming Screeps
tags: Series
excerpt_separator: <!--more-->
---

Recently I felt like revisiting a programming game that I've dabbled with in the past. The last time I played I wasn't 
really familiar with things like unit testing and after a while it made maintaining my code increasingly difficult, to 
the point where I simply ran out of time to keep up with it.

I've grown a lot as a programmer since then and I feel like it's time to give it another go as it's a great way to 
practice and have fun at the same time.

<!--more-->

## What is Screeps?

Screeps is a really interesting game aimed at programmers, it has you write code to act as the ai for a colony of bots 
(Creeps). I'm not going to go into much more detail here, but it's definitely worth checking out here: 
[https://screeps.com](https://screeps.com)
There have been a bunch of new features added since I last played. So while I kind of know what I'm doing at the start, 
I think that I'm pretty quickly going to be coming across new mechanics I've not seen before, which will make for 
interesting challenges.

## The plan

Something I struggled with last time I played this game was a lack of direction. I went straight from the tutorial 
(which is very worthwhile doing) and continued to build upon the same code as I grew my colony. I found this to be a 
great way to get my feet wet, but eventually it started to become obvious that I was spending way too much time fixing 
unforeseen bugs caused by new functionality. 

This time I want to take a different approach that I'm hoping will keep things a bit more under control.

For a start I'm going to be using a [TDD](https://en.wikipedia.org/wiki/Test-driven_development) approach this time 
around. This should make it much easier to add new functionality while ensuring I'm not breaking anything as the 
codebase grows. It will also force me to put a bit more thought into the code I'm writing and keep things simple.

Secondly, I'm going to be modelling my ai in a similar way to an operating system. From what I can see, this is a pretty
widely used approach to writing Screeps ai and has many benefits over the tutorial approach. Rather than iterating 
through each of my creeps and deciding what they're going to do, I want to maintain a list of jobs that need to be 
done. Then the most appropriate creep can be assigned to that job. The idea is that each of these jobs will be 
responsible for doing one very specific thing. If it needs to do something else, it will create a new job to take care 
of it and wait for it to finish, much like a process.

## What to expect

I'm going to try to post about all major design decisions and interesting events in game. I will try to dive deeper into
specific code implementation now and then, but I want to make sure I can progress at a reasonable rate without getting 
bogged down in writing (I'm VERY slow at putting out posts...)

As I want this to be a series, I wanted to put out this introduction before diving in. My next post will be a more 
detailed look at the first core component I need to implement. 