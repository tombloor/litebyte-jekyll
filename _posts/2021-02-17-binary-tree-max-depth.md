---
layout: post
title:  "Leetcode 104: Maximum Depth of Binary Tree"
date:   2022-02-18 18:00:00 -0500
categories: Programming Problems
tags: Python Binary-Tree Leetcode
excerpt_separator: <!--more-->
---

Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf
node.

<!--more-->

To view this problem on Leetcode [Click Here](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/){:target="_blank"}
The key to solving this problem is a fundamental understanding of the binary tree data structure and its traversals.

In simple terms, a binary tree is a tree data structure in which each node has at most two child nodes. The depth of a
node in the tree is it's vertical distance from the root. See the tree below for an example:

```
            5        -- Depth 0
          /   \
         1     2     -- Depth 1
              / \
             3   9   -- Depth 2
```

The question is asking us to find the maximum depth of the entire tree. To do this, we are going to have to make our way
from the root (the top) of the tree, all the way down to the deepest node we can find. Once we're sure that there are no
deeper nodes, we can return the current depth as our answer.

Let's start by looking at how we can traverse the nodes of the tree. As we're looking to find the deepest node, it would
make sense to use a [depth first search](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/){:target:"_blank"}
. A depth first search (DFS) visits each child of a node, before visiting the node itself. This process can be called
recursively until every node has been visited. Using the example above, the steps would be:

1. Start at the root (5)
2. Visit the left child (1)
3. (1) has no children, so we go back up to (5)
4. Visit the right child (2)
5. Visit the left child (3)
6. (3) has no children, so we go back up to (2)
7. Visit the right child (9)

Once we have this traversal in place the only other thing we need to do is to keep track of the maximum depth we've 
seen. At this point I think it actually helps to stop referring to a nodes depth. Instead we will try to find each nodes
height, meaning it's vertical distance from the lowest node on the tree. The resulting answer is the same.

Let's look at the same example again, but this time I'll label each node with it's height in the tree.

```
               5  (Height 3)
             /   \
(Height 1)  1     2  (Height 2)
                 / \
    (Height 1)  3   9  (Height 1)
```

Looking at this example, we can draw the conclusion that the height of a node is equal to 1 + the larger of the height of 
it's children. Or `height = 1 + max(leftHeight, rightHeight)`. To find the left and right heights we can recursively
call the same function until we run out of nodes, at which point we will return 0.

{% highlight python linenos %}
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))
{% endhighlight %}
