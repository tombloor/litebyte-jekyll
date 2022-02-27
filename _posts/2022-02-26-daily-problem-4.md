---
layout: post
title:  "Daily Coding Problem #4"
date:   2022-02-26 23:00:00 -0500
categories: Programming Problems
tags: Python Series
excerpt_separator: <!--more-->
---

Continuing my mission to keep up with the Daily Coding Problems for as long as I can. Day 4.

<!--more-->

## Today's problem

>Good morning! Here's your coding interview problem for today.
>
>This problem was asked by Stripe.
>
>Given an array of integers, find the first missing positive integer in linear time and constant space. In other words, find the lowest positive integer that does not exist in the array. The array can contain duplicates and negative numbers as well.
>
>For example, the input [3, 4, -1, 1] should give 2. The input [1, 2, 0] should give 3.
>
>You can modify the input array in-place.

*If you're interested in practicing your problem solving too you can sign up for the 
[Daily Coding Problem](https://www.dailycodingproblem.com/) for free.*

## Solution

This was a tricky one, the time and space complexity constraints meant that my initial ideas of sorting the array or
using a hashmap wouldn't work. In the end this problem was solved in three passes through the array:

1. In the first pass we swap all of the non-positive values (0 or less) to the front of the array. The purpose of this
is to separate them from the values we need to search through.
2. On the second pass through the array we set `array[i]` to be a negative number, to mark that this number is not
missing.
3. On the final pass through the array, we return the index of the first positive number. This must be the missing
number as otherwise it would have been set to negative in step 2.
4. If there are no positive numbers, then the result is the number of positive numbers in the array, plus one (the
missing number was at the end of the array).

{% highlight python linenos %}
def solve(arr):
    # Move all negative and zero to the start of the array
    pos_idx = 0
    for i in range(len(arr)):
        if arr[i] <= 0:
            arr[i], arr[pos_idx] = arr[pos_idx], arr[i]
            pos_idx += 1

    # Iterate through the array and set the idx of each number to negative
    for i in range(pos_idx, len(arr)):
        abs_item = abs(arr[i])
        if abs_item < len(arr):
            arr[abs_item] = abs(arr[abs_item]) * -1

    # Return the index of the first positive number
    for i in range(pos_idx, len(arr)):
        if arr[i] > 0:
            return i

    return i + 1
{% endhighlight %}

*Is there a problem with my solution? please [open an issue](https://github.com/tombloor/daily-coding-problems/issues/new?title=Problem%204) and let me know!*
