---
layout: post
title:  "The Hourglass Problem"
date:   2021-10-26 08:00:00 -0500
categories: Programming Problems
tags: Python Arrays HackerRank
excerpt_separator: <!--more-->
---

Given a 6x6 2d array, find the maximum sum of all the hourglasses.

... Ok so this problem doesn't make much sense without some more context. In this post I'll walk through how I tackled
the `2D Array - DS` problem on [HackerRank](https://www.hackerrank.com). It's a fairly straightforward one to solve, so 
it shouldn't take long to work through.

<!--more-->

[Click Here](https://www.hackerrank.com/challenges/2d-array/problem) to go to the problem to see it for yourself

## The Solution

In this problem we are given a 6x6 2d array of integers and have been tasks with finding the largest possible sum of
numbers arranged in an hour glass pattern. Given that the array is small, and is always going to be the same size, 
performance is probably not going to be a major factor. Therefore in my opinion the best solution will be one that 
favours simplicity. 

The first step in this solution is to figure out how we can identify which numbers belong to each hourglass. I began by
deciding on an anchor to build each shape around. I decided on the middle number as it split the shape nicely in half,
you could pick a different anchor if you want, but this one made sense to me and kept things simple later on.

<div class='row'>
    <pre class='col'>
        <code>
        data = [
            [ <strong style='color:red'> 2  1  9</strong> -2 -3  2 ],
            [ -1 <strong style='color:red'> 1</strong>  3  8  8  5 ],
            [ <strong style='color:red'>-4  5  4</strong>  1  5  9 ],
            [  2  5  4  2  3  9 ],
            [  8  9  4 -6  6 -5 ],
            [  0  2  0  0 -8  8 ]
        ]
        </code>
    </pre>
    <pre class='col'>
        <code>
        data = [
            [  2  1  9 -2 -3  2 ],
            [ -1  1  3  8  8  5 ],
            [ -4  5<strong style='color:red'>  4  1  5</strong>  9 ],
            [  2  5  4<strong style='color:red'>  2</strong>  3  9 ],
            [  8  9<strong style='color:red'>  4 -6  6</strong> -5 ],
            [  0  2  0  0 -8  8 ]
        ]   
        </code>
    </pre>
</div>

Looking at the examples above, we can see that an hourglass can be split into three components.

- Top bar
- Center (Also our anchor)
- Bottom bar

For each of these components it's easy to write an expression to find the indices it is comprised of. Assuming `(i, j)` 
refers to the position of a number by ('column', 'row'), and that our anchor is at `(0,0)`, we can define the components
as follows:

- Top bar = `data[j-1][i-1]`, `data[j-1][i]` and `data[j-1][i+1]`
- Center = `data[j][i]`
- Bottom bar = `data[j+1][i-1]`, `data[j+1][i]` and `data[j+1][i+1]`

(If you're more mathematically inclined, it can sometimes help if you substitute `(i, j)` for `(x, y)`)

What you will have probably noticed at this stage is that because each bar extends +-1 column and row out from our
anchor, we will never be able to create an hourglass when `j=0` or `j=5`, similarly we will never be able to create an
hourglass when `i=0` or `i=5`. This is something we need to keep in mind as we set up our loops as we don't want to try
and build an hourglass that doesn't fit.

Ordinarily we would set up this nested loop if we wanted to iterate through a 6x6 2d array: 

{% highlight python linenos %}
for i in range(0, 6):
    for j in range(0, 6):
        hourglass_sum(i, j)
{% endhighlight %}

However, in this case we don't want to iterate the outer edges of the array, as we won't be able to fit an hourglass 
there. A slight tweak to our loop make sure we don't step out of bounds:

{%comment%}add line_highlight=1,2{%endcomment%}
{% highlight python linenos %}
for i in range(1, 5):
    for j in range(1, 5):
        hourglass_sum(i, j)
{% endhighlight %}

Now that we have the expressions required to build an hourglass at a given point in the array, and an idea of the 
boundaries for our loops, we can work through a couple of iterations by hand to see how things play out.

{% highlight text %}
First Hourglass 
i = 1
j = 1
max_sum = 0

top = 2 + 1 + 9 = 12
center = 2
bottom = -4 + 5 + 4 = 5
total = 19
max_sum = max(max_sum, total) = 19

Second Hourglass
i = 1
j = 2

top = 1 + 9 + -2 = 8
center = 3
bottom = 5 + 4 + 1 = 10
total = 21
max_sum = max(max_sum, total) = 21
{% endhighlight %}

It looks like this approach will work, by the time we have hit the end of our loop we will have calculated the sum for
every hourglass and because we are keeping track of the maximum sum encountered so far we can just return that at the
end. The time complexity for this solution is pretty straightforward, we are iterating once through each item, in each 
array. We can express this as `O(nm)` where `n` is the number of arrays and `m` is the number of items in the array.

{% highlight python linenos %}
def hourglassSum(arr):
    max_sum = None

    for y in range(1, len(arr) - 1): # End bound not inclusive
        row = arr[y]
        for x in range(1, len(row) - 1):
            top = sum([i for i in arr[y-1][x-1:x+2]]) # End bound not inclusive
            middle = arr[y][x]
            bottom = sum([i for i in arr[y+1][x-1:x+2]]) # End bound not inclusive

            curr_sum = sum([top, middle, bottom])
            max_sum = max(max_sum, curr_sum) if max_sum is not None else curr_sum

    return max_sum
{% endhighlight %}
