### 1. Problem Description
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

### 2. Solutions
Define rob(n) to be the maximum amount to rob as we pass a house.
- Optimal structure
```
rob(n)
= max(rob(n - 1), rob(n - 2) + nums[i])
```
- Recurrence
```
rob(-2) = 0
rob(-1) = 0
rob(0) = max(rob(- 1), rob(- 2) + nums[0])
rob(1) = max(rob(0), rob(-1) + nums[1])
rob(2) = max(rob(1), rob(0) + nums[2])
rob(3) = max(rob(2), rob(1) + nums[i])
......
```
- Code
```python
class Solution:
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        robs = [0, 0]

        for i in range(len(nums)):
            robs.append(max(robs[-2] + nums[i], robs[-1]))

        return robs[-1]
```
```python
class Solution:
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        rob, notrob = 0, 0

        for i in range(len(nums)):
            rob_curr = notrob + nums[i]
            notrob = max(rob, notrob)
            rob = rob_curr

        return max(rob, notrob)
```
