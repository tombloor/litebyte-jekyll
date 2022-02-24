---
layout: post
title:  "Daily Coding Problem #1"
date:   2022-02-23 18:00:00 -0500
categories: Programming Problems
tags: Python Series
excerpt_separator: <!--more-->
---

I recently came across the Daily Coding Problem email list. I'm trying to get faster at writing up coding problems and
this seemed like a good way to get some practice. I probably won't be able to post one of these every single day, but 
I'm curious to see how long I can keep up.

I received the first problem this morning and I'm starting off strong with a write up on the same day.

<!--more-->

## Today's problem

>Good morning! Here's your coding interview problem for today.
>
>This problem was recently asked by Google.
>
>Given a list of numbers and a number k, return whether any two numbers from the list add up to k.
>
>For example, given [10, 15, 3, 7] and k of 17, return true since 10 + 7 is 17.
>
>Bonus: Can you do this in one pass?

*If you're interested in practicing your problem solving too you can sign up for the 
[Daily Coding Problem](https://www.dailycodingproblem.com/) for free.*

## Solution

This is a nice simple problem to get started, one that I've seen before when working through 
[Leetcode](https://leetcode.com/) and other similar services.

The process for solving the problem is as follows:
1. Iterate through each item in the array
2. Subtract the item from the target number to find the compliment (the number we would need to add to get the target)
3. Check if we have seen this compliment earlier in the array, if yes return true, else continue
4. Add the current item to a set of compliments so we can quickly check against future values in the array.
5. If we get to the end of the array and we still haven't found a matching compliment we can return false.

The really important part of this process is storing each value in a set as we move through the array. The set allows us
to lookup each compliment in constant time while moving through the array only once. Without it we would have to keep 
scanning through the array repeatedly for each item.


{% highlight python linenos %}
def solve(arr, k):
    compliments = set()
    for n in arr:
        c = k - n
        if c in compliments:
            return True
        compliments.add(n)
    return False
{% endhighlight %}

*Is there a problem with my solution? please [open an issue](https://github.com/tombloor/daily-coding-problems/issues/new?title=Problem%201) and let me know!*