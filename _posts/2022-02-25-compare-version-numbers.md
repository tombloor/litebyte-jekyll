---
layout: post
title:  "Leetcode 165: Compare Version Numbers"
date:   2022-02-25 12:20:00 -0500
categories: Programming Problems
tags: Python Recursion Leetcode
excerpt_separator: <!--more-->
---

Given two version numbers, version1 and version2, compare them.

<!--more-->

To view the full question on Leetcode [click here](https://leetcode.com/problems/compare-version-numbers/){:target="_blank"}.

To summarise, we are given two version numbers in the format `a.b.c` where `a`, `b` and `c` are integers. Each component
of the version number may or may not have leading zeroes, however these should be ignored when comparing values. If one
of the version numbers is missing one of the components, for example if we were comparing `1.0` to `1.0.0`, it should be
considered as if it were zero.

The expected output is `1` if version 1 is greater than version 2, `-1` if version 2 is greater, or `0` if they are
equal.

## The Solution

Looking at this problem it became apparent to me that we could split this into a series of sub problems. 

If we start by looking at the first component of each number and see that one is greater than the other, then we don't 
have to bother with looking through the rest of the components as they would have no effect on the result.

```
version1 = 1.6.0
version2 = 2.0.0

Looking at the first components, 2 > 1. Therefore version2 is greater than version1
```

If the first component of each version number is equal, then we can discard it and move on to the next component.

We can repeat this process until we find one component that is larger than the other, or we run out of components. If 
we run out, we know that the version numbers are equal.

I chose to implement this recursively as seen below. One important thing to remember is that if one of the version
numbers is missing a component, it should be treated as if it were zero.

{% highlight python linenos %}
class Solution:
    def compareVersion(self, version1: str, version2: str) -> int:
        if version1 == '' and version2 == '':
            return 0
        
        if version1 == '':
            version1 = '0'
        if version2 == '':
            version2 = '0'
        
        v1_split = version1.split('.')
        v2_split = version2.split('.')
        
        v1 = int(v1_split.pop(0))
        v2 = int(v2_split.pop(0))
        
        if v1 > v2:
            return 1
        if v2 > v1:
            return -1
        
        return self.compareVersion('.'.join(v1_split), '.'.join(v2_split))
{% endhighlight %}
