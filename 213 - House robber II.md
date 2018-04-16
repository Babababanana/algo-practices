### 1. Problem Description
Note: This is an extension of House Robber.

After robbing those houses on that street, the thief has found himself a new place for his thievery so that he will not get too much attention. This time, all houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, the security system for these houses remain the same as for those in the previous street.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

### 2. Solutions
##### 2.1 Solution
Since the first and last element are seen as adjacent, there are only 3 cases in the chosen solution:
1. first house robbed and last not
2. first element not robbed and last robbed
3. both not robbed

Run the house robber I algorithm for the following two inputs:
1. excluding the first house
2. excluding the last house

The most optimal one will be the larger outcome.
```python
class Solution:
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) == 1:
            return nums[0]

        robs1 = [0, 0]
        robs2 = [0, 0]

        for num in nums[1::]:
            robs1.append(max(robs1[-2] + num, robs1[-1]))

        print(nums[:-1])
        for num in nums[:-1:]:
            robs2.append(max(robs2[-2] + num, robs2[-1]))

        return max(robs1[-1], robs2[-1])
```
