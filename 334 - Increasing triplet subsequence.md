### 1. Problem Description
Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.

Formally the function should:

Return true if there exists i, j, k
such that arr[i] < arr[j] < arr[k] given 0 ≤ i < j < k ≤ n-1 else return false.

Your algorithm should run in O(n) time complexity and O(1) space complexity.

- Input: List[int]
- Output: bool

#### Edge cases
1. Length of input is less than 3
  - return false

#### 2.1 Analysis
In this problem, we only care about if the subsequence exists.

### 3. Solutions
#### 3.1 Solution 1
##### Analysis
Steps:
1. Traverse over the given numbers
2. Find the smallest number and the second smallest number in the visited numbers, and keep updating them as we iterate.
3. See if there is another number in the unvisited part that is greater than the stored second smallest number, if yes return true, if there no such number found after visiting the entire list, return false.

Runtime:
- T = O(n)

##### Code
```python
class Solution:
    def increasingTriplet(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        min1 = min2 = float('inf')

        for num in nums:
            if num <= min1:
                min1 = num
            elif num <= min2:
                min2 = num
            else:
                return True
        return False
```
#### 3.2 Solution 2
##### Steps
##### Code
```python
```
