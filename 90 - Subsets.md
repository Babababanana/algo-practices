### 1. Problem Description
Given a collection of integers that might contain duplicates, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

For example,
If nums = [1,2,2], a solution is:
```
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```


### 2. Solutions
##### 2.1 DP (56ms)
1. Sort the nums list
2. For each number in nums, concatenate it with previously obtained subsets
3. Add each concatenation back to the subsets if it doesn't already exist
4. Finally add the empty subset ```[]```

By sorting nums first, we can avoid duplicates when a number appears multiple times in different locations. For example:
```
Input: [4,4,1,4]

Output:
1. Sorted
[[1],[4],[1,4],[4,4],[1,4,4],[4,4,4],[1,4,4,4],[]]

2. Not sorted
[[4],[4,4],[1],[4,1],[4,4,1],[4,4,4],[1,4],[4,1,4],[4,4,1,4],[]]
Duplicates:
[4,1], [1,4]
[4,4,1], [4,1,4]
```

```python
class Solution:
    def subsetsWithDup(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        subsets = []

        for n in nums:
            temp = []
            if [n] not in subsets:
                temp.append([n])
            for s in subsets:
                if s + [n] not in subsets:
                    temp.append(s + [n])
            subsets += temp
        subsets.append([])
        return subsets
```
