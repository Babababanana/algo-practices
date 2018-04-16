### 1. Problem Description
Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6.

### 2. Solutions
##### 2.1 Brute force
Find the sum for all possible subarrays and return the maximum

Rumtime = O(n ^ 2)

**Time limit exceeded**

```python
class Solution:
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        s = []

        for i in range(n):
            for j in range(i, n):
                s.append(sum(nums[i:j + 1]))
        return max(s)

```
##### 2.2 Kadane's algorithm
1. Keep track of the maximum subarray for the nums[:i] - global max ```gl_max```
2. The maximum subarray including nums[i] is ```curr_max = max(nums[i], curr_max + nums[i])```
3. ```gl_max = max(curr_max, gl_max)```

Runtime: O(n)

```python
class Solution:
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0

        curr_max = gl_max = nums[0]

        for i in range(1, len(nums)):
            curr_max = max(nums[i], curr_max + nums[i])
            if curr_max >= gl_max:
                gl_max = curr_max

        return gl_max
```
