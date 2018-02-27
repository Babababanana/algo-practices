### 1. Problem Description
Rotate an array of n elements to the right by k steps.

For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].

### 2. Solutions
#### 2.1 Solution 1
##### Analysis
When k == len(nums), the array remains the same. How many shifts needed depends on the residual k % len(nums).

Steps:
1. Initialize an auxiliary array l same a s the given array nums
2. Iterate through l and assign each number in l to the right position in nums

Runtime:
T(n) = O(n)

```python
class Solution:
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        l = [num for num in nums]

        for idx, num in enumerate(l):
            nums[idx + k % len(l) - len(l)] = num
```

#### 2.2 Solution 2
##### Analysis

##### Code
```python
class Solution:
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: void Do not return anything, modify nums in-place instead.
        """        
        n = len(nums)
        k = k % n
        nums[:k], nums[k:] = nums[(n-k):], nums[:(n-k)]
```

#### 2.3 Solution 3
##### Analysis

##### Code
```python
class Solution:
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: void Do not return anything, modify nums in-place instead.
        """        
        def reverse(arr, i, j):
            while i < j:
                temp = arr[i]
                arr[i] = arr[j]
                arr[j] = temp
                i += 1
                j -= 1

        if len(nums) > 1:
            k = k % len(nums)

            reverse(nums, 0, len(nums) - k - 1)
            reverse(nums, len(nums) - k, len(nums) - 1)
            reverse(nums, 0, len(nums) - 1)
```
