### 1. Problem Description
Given a non-empty binary tree, return the average value of the nodes on each level in the form of an array.

### 2. Solutions
#### 2.1 Solution 1
##### Analysis
Steps:
1. Non-recursive BFS traverse
2. Average the node values in the queue
3. Create a empty temp queue and enqueue all child nodes of the nodes on the current level
4. Replace the old queue by the temp queue

Runtime:
- T(n) = theta(n)

##### Code
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def averageOfLevels(self, root):
        """
        :type root: TreeNode
        :rtype: List[float]
        """
        res = []

        queue = [root]

        while queue:
            res.append(sum([node.val for node in queue])/len(queue))

            temp_queue = []

            for node in queue:
                if node.left:
                    temp_queue.append(node.left)
                if node.right:
                    temp_queue.append(node.right)
            queue = temp_queue

        return res
```
