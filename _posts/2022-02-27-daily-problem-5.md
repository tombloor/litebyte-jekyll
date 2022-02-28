---
layout: post
title:  "Daily Coding Problem #5"
date:   2022-02-27 23:00:00 -0500
categories: Programming Problems
tags: Python Series
excerpt_separator: <!--more-->
---

Continuing my mission to keep up with the Daily Coding Problems for as long as I can. Day 5.

<!--more-->

## Today's problem

>Good morning! Here's your coding interview problem for today.
>
>This problem was asked by Jane Street.
>
>cons(a, b) constructs a pair, and car(pair) and cdr(pair) returns the first and last element of that pair. For example, car(cons(3, 4)) returns 3, and cdr(cons(3, 4)) returns 4.
>
>Given this implementation of cons:
>
>```
>def cons(a, b):
>    def pair(f):
>        return f(a, b)
>    return pair
>```
>
>Implement car and cdr.

*If you're interested in practicing your problem solving too you can sign up for the 
[Daily Coding Problem](https://www.dailycodingproblem.com/) for free.*

## Solution

This problem is a test in your understanding of functional programming. If we break down what is going on in the 
provided `cons` function, we can see that it returns another function (`pair`) which expects a function (`f`) as an 
argument. This final function expects our `a` and `b` values as arguments. It's pretty easy to get lost with so many
functions being passed around, but once you see what it's doing it's pretty easy to get to a solution.

{% highlight python linenos %}
def cons(a, b):
    def pair(f):
        return f(a, b)
    return pair

def car(pair):
    def left(a, b):
        return a
    return pair(left)

def cdr(pair):
    def right(a, b):
        return b
    return pair(right)
{% endhighlight %}

*Is there a problem with my solution? please [open an issue](https://github.com/tombloor/daily-coding-problems/issues/new?title=Problem%205) and let me know!*
