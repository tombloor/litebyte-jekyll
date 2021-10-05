---
layout: post
title:  "The Hourglass Problem"
date:   2021-08-27 09:00:00 -0500
categories: Programming Problems
tags: python arrays
excerpt_separator: <!--more-->
---

Given a 6x6 2d array, find the maximum sum of all the hourglasses.

... Ok so this problem doesn't make much sense without some more context. In this post I'll walk through how I tackled
the `2D Array - DS` problem on [HackerRank](https://www.hackerrank.com). It's a fairly straightforward one to solve,
but I wanted to ease into these write ups, so this was a good place to start.

<!--more-->

## Preamble

I've recently been trying to dedicate some time each week working on programming challenges or personal projects.
Finding time to program outside of work can sometimes be a challenge, but I've found it refreshing to be able to sit
down for 20-30 minutes and write some code unrelated to my job. It's definitely something I want to try to do more 
often.

After I'd worked through a couple of these problems, I felt it would be a good to write them up as full walkthroughs.
At the time of writing this post I have been working professionally as a developer for around 8 years, and I can 
honestly say I've never experienced anything like many of these challenges in a real-world scenario. However they are 
still fun and interesting to work through, and they often lead to exploring new ideas and techniques that I may not be
exposed otherwise.

[Click Here](https://www.hackerrank.com/challenges/2d-array/problem) to go to the problem to see it for yourself

## The Solution

In this problem we are given a 6x6 2d array of integers and have been tasks with finding the largest possible sum of
numbers arranged in an hour glass pattern. Given that the array is small, and is always going to be the same size, 
performance is probably not going to be a major factor. Therefore in my opinion the best solution will be one that 
favours simplicity. 

The first step in this solution is to figure out how we can identify which numbers belong to each hourglass. I began by
deciding on an anchor to build each shape around. I decided on the middle number as it split the shape nicely in half,
you could pick a different anchor if you want, but this one made sense to me and kept things simple later on.

<figure class='text-center'>
    <img class="text-center" src="/assets/img/blog/hourglass-1.png" />
</figure>

Looking at the image above, we can see that an hourglass can be split into three components.
- Center (Also our anchor)
- Top bar
- Bottom bar

For each of these components it's easy to write an expression to find the numbers it is comprised of. Assuming `(i, j)` 
refers to the position of a number by ('column', 'row'), and that our anchor is at `(0,0)`, we can define the components
as follows:

- Center = `arr[j][i]`
- Top bar = `arr[j-1][i-1]`, `arr[j-1][i]` and `arr[j-1][i+1]`
- Bottom bar = `arr[j+1][i-1]`, `arr[j+1][i]` and `arr[j+1][i+1]`

(If you're more mathematically inclined, it can sometimes help if you substitute `(i, j)` for `(x, y)`)

What you will have probably noticed at this stage is that because each bar extends +-1 column and row out from our
anchor, we will never be able to create an hourglass when `j=0` or `j=5`, similarly we will never be able to create an
hourglass when `i=0` or `i=5`. This is something we need to keep in mind as we set up our loops as we don't want to try
and build an hourglass that doesn't fit.

<figure class='text-center'>
    <img class="text-center" src="/assets/img/blog/hourglass-2.png" />
</figure>

Ordinarily we would set up this nested loop if we wanted to iterate through a 6x6 2d array: 

{% highlight python linenos %}
for i in range(0, 6):
    for j in range(0, 6):
        do_the_work()
{% endhighlight %}

However, in this case we don't want to iterate the outer edges of the array, as we won't be able to fit an hourglass 
there. A slight tweak to our loop make sure we don't step out of bounds:

{%comment%}add line_highlight=1,2{%endcomment%}
{% highlight python linenos %}
for i in range(1, 5):
    for j in range(1, 5):
        do_the_work()
{% endhighlight %}

Now that we have the expressions required to build an hourglass at a given point in the array, and an idea of the 
boundaries for our loops, we can work through a couple of iterations by hand to see how things play out.
-- WORK THROUGH SOME ITERATIONS HERE

-- Sum of one hourglass

-- Store the current max sum

-- PYTHON GOTCHA!!! When max_sum = None, couldn't start at 0 because of negs, so we have to explicitly check for None

-- Conclusion
