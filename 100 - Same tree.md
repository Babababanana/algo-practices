### 1. Problem Description
Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.


Example 1:
```
Input:     1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

Output: true
```
Example 2:
```
Input:     1         1
          /           \
         2             2

        [1,2],     [1,null,2]

Output: false
Example 3:

Input:     1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

Output: false
```

### 2. Solutions
##### 2.1 DFS with stack
Compare current nodes of the two trees and their children
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSameTree(self, p, q):
        """
        :type p: TreeNode
        :type q: TreeNode
        :rtype: bool
        """

        curr1 = None
        curr2 = None
        stack1 = [p]
        stack2 = [q]

        while(stack1 and stack2):
            curr1 = stack1.pop()
            curr2 = stack2.pop()

            if curr1 and curr2:
                if curr1.val != curr2.val:
                    return False
            elif curr1 == curr2 == None:
                return True
            else:
                return False

            if curr1.right and curr2.right:
                if curr1.right.val != curr2.right.val:
                    return False
                else:
                    stack1.append(curr1.right)
                    stack2.append(curr2.right)
            elif curr1.right != curr2.right:
                return False

            if curr1.left and curr2.left:
                if curr1.left.val != curr2.left.val:
                    return False
                else:
                    stack1.append(curr1.left)
                    stack2.append(curr2.left)
            elif curr1.left != curr2.left:
                return False

        return True
```
##### 2.2 Recursion
The ```is``` operator is to test reference equality. In this case is to see if both p and q are None, because p and q won't be referring to the same object.
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSameTree(self, p, q):
        """
        :type p: TreeNode
        :type q: TreeNode
        :rtype: bool
        """

        if p and q:
            return p.val == q.val and self.isSameTree(p.right, q.right) and self.isSameTree(p.left, q.left)
        return p is q
```
