---
layout: post
title:  "Daily Coding Problem #3"
date:   2022-02-25 18:00:00 -0500
categories: Programming Problems
tags: Python Series
excerpt_separator: <!--more-->
---

Continuing my mission to keep up with the Daily Coding Problems for as long as I can. Day 3.

<!--more-->

## Today's problem

>Good morning! Here's your coding interview problem for today.
>
>This problem was asked by Google.
>
>Given the root to a binary tree, implement serialize(root), which serializes the tree into a string, and deserialize(s), which deserializes the string back into the tree.
>
>For example, given the following Node class
>
>```
>class Node:
>    def __init__(self, val, left=None, right=None):
>        self.val = val
>        self.left = left
>        self.right = right
>```
>The following test should pass:
>```
>node = Node('root', Node('left', Node('left.left')), Node('right'))
>assert deserialize(serialize(node)).left.left.val == 'left.left'
>```

*If you're interested in practicing your problem solving too you can sign up for the 
[Daily Coding Problem](https://www.dailycodingproblem.com/) for free.*

## Solution

Today we have a medium difficulty problem. In this one it really helps to have a solid understanding of the fundamentals
of a binary tree. First we'll look at the process for serializing the tree to a string, this is simply a pre-order
traversal ([learn about tree traversals here](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/){:target="_blank"}).
The steps are as follows:

1. If the current node is not empty
    1. Add the current node to the return array. If the node is null, add an empty string
    2. Recursively call serialize on the nodes left child
    3. Recursively call serialize on the nodes right child
2. If the current node is empty, push an empty string to the return array
3. Return the array as a comma separated string

{% highlight python linenos %}
def _serialize_helper(root):
    results = []
    if not root:
        results.append('')
    else:
        results.append(root.val)
        results += _serialize_helper(root.left)
        results += _serialize_helper(root.right)
    return results

def serialize(root):
    results = _serialize_helper(root)
    return ','.join(results)
{% endhighlight %}

*Is there a problem with my solution? please [open an issue](https://github.com/tombloor/daily-coding-problems/issues/new?title=Problem%203%20(Serialize)) and let me know!*


The steps to deserialize the string back into a tree are pretty similar. The major difference is that we need to keep
track of the current index in the array as we build the nodes. This is so when we hit the empty leaf nodes and start
moving back up the tree to fill out the next branch we keep our place in the array.

{% highlight python linenos %}
def _deserialize_helper(arr, idx):
    if arr[idx] == '':
        return None, idx
    
    n = Node(arr[idx])
    n.left, idx = _deserialize_helper(arr, idx + 1)
    n.right, idx = _deserialize_helper(arr, idx + 1)

    return n, idx

def deserialize(s):
    arr = s.split(',')
    result, _ =  _deserialize_helper(arr, 0)
    return result
{% endhighlight %}

*Is there a problem with my solution? please [open an issue](https://github.com/tombloor/daily-coding-problems/issues/new?title=Problem%203%20(Deserialize)) and let me know!*
