### 1. Problem Description
Given a collection of distinct numbers, return all possible permutations.

For example,
[1,2,3] have the following permutations:
```
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

### 2. Solutions
##### 2.1 Backtracking
Create a helper function to take available and chosen numbers and append the chosen numbers to result when no number is available.
```python
class Solution:
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        def helper(ava, chosen):
            if not ava:
                res.append(chosen)
            else:
                for i in range(len(ava)):
                    n = ava.pop(i)
                    helper(ava, chosen + [n])
                    ava.insert(i, n)

        res = []
        helper(nums, [])
        return res

```
```python
class Solution:
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """        
        res = [[]]
        for n in nums:
            temp = []
            for chosen in res:
                temp += [chosen + [ava] for ava in nums if ava not in chosen]
            res = temp
        return res
```
