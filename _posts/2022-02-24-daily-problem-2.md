---
layout: post
title:  "Daily Coding Problem #2"
date:   2022-02-23 18:00:00 -0500
categories: Programming Problems
tags: Python Series
excerpt_separator: <!--more-->
---

Continuing my mission to keep up with the Daily Coding Problems for as long as I can.

<!--more-->

## Today's problem

>Good morning! Here's your coding interview problem for today.
>
>This problem was asked by Uber.
>
>Given an array of integers, return a new array such that each element at index i of the new array is the product of all
>the numbers in the original array except the one at i.
>
>For example, if our input was [1, 2, 3, 4, 5], the expected output would be [120, 60, 40, 30, 24]. If our input was 
>[3, 2, 1], the expected output would be [2, 3, 6].

*If you're interested in practicing your problem solving too you can sign up for the 
[Daily Coding Problem](https://www.dailycodingproblem.com/) for free.*

## Solution

This is listed as a hard difficulty problem. With a little thought its actually a very simple problem to solve (you will
see why it is listed as hard in the next section)

The simplest approach to solve this problem is as follows:

1. Find the product of the entire array.
2. Iterate through the array and divide the total product by the current value.
3. Push the result to the output array.

In code it could look something like this.

{% highlight python linenos %}
import math

def solve(arr):
    total = math.prod(arr)
    result = []
    
    for n in arr:
        result.append(total / n)

    return result
{% endhighlight %}

*Is there a problem with my solution? please [open an issue](https://github.com/tombloor/daily-coding-problems/issues/new?title=Problem%202) and let me know!*

## Follow up

Now this is where the problem gets a bit more tricky.

>Follow-up: what if you can't use division?

We're going to have to take a different approach now that the computer has forgotten how to use division. I had a couple
of ideas with this new restriction and I'm pretty satisfied with the approach I ended up with. 

The idea came to me when I expressed the problem as `n = prod(arr[0]...arr[n-1]) * prod(arr[n+1]...)`. In plain english,
to get the correct value we need to know the total product of all the values to the left, and right of it. After looking
at it for a bit longer, I came up with this 2 step process:

1. Iterate forward through the array, setting `result[i]` to the cumulative product of all the values before it.
2. Iterate backward through the array, multiplying `result[i]` by the cumulative product of all the values after it.

Looking at the code below, you can see how I achieved this using a temporary variable to hold the current cumulative
product for each step.

{% highlight python linenos %}
def solve_followup(arr):
    result = [1 for n in range(0, len(arr))]
    tmp = 1

    # Iterate forward - filling cumulative product of arr[0] -> arr[i]
    for i in range(0, len(arr)):
        result[i] = tmp
        tmp *= arr[i]
    
    tmp = 1
    # Iterate backward - filling with cumulative product of arr[-1] -> arr[i] 
    for i in range(1, len(arr) + 1):
        result[-i] = tmp * result[-i]
        tmp *= arr[-i]

    return result
{% endhighlight %}

*Is there a problem with my solution? please [open an issue](https://github.com/tombloor/daily-coding-problems/issues/new?title=Problem%202%20(Followup)) and let me know!*
