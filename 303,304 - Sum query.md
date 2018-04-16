# Sum Query

## 1. 303 Range Sum Query - Immutable
### 1.1 Problem Description
Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

Example:
```
Given nums = [-2, 0, 3, -5, 2, -1]

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
```

Note:
You may assume that the array does not change.
There are many calls to sumRange function.

### 1.2 Solutions
##### 1.2.1 Array solution
1. Initiate NumArray's array as the input array
2. Sum self.nums[i:j + 1] if the inverval is valid

```python
class NumArray:

    def __init__(self, nums):
        """
        :type nums: List[int]
        """
        self.nums = nums


    def sumRange(self, i, j):
        """
        :type i: int
        :type j: int
        :rtype: int
        """
        l = len(self.nums)

        if i < 0 or j >= l:
            return 0
        return sum(self.nums[i:j + 1])


# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# param_1 = obj.sumRange(i,j)
```

##### 1.2.2 DP solution
1. Initiate NumArray's array as the sum from index 0 to current index

```python
class NumArray:

    def __init__(self, nums):
        """
        :type nums: List[int]
        """
        self.nums = nums
        for i in range(1, len(nums)):
            self.nums[i] += self.nums[i - 1]


    def sumRange(self, i, j):
        """
        :type i: int
        :type j: int
        :rtype: int
        """
        if i < 0 or j >= len(self.nums):
            return 0
        return self.nums[j] - (self.nums[i - 1] if i > 0 else 0)


# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# param_1 = obj.sumRange(i,j)
```

## 2. 304 Range Sum Query 2D - Immutable
### 2.1 Problem Description
Given a 2D matrix matrix, find the sum of the elements inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).

Range Sum Query 2D
The above rectangle (with the red border) is defined by (row1, col1) = (2, 1) and (row2, col2) = (4, 3), which contains sum = 8.

Example:
```
Given matrix = [
  [3, 0, 1, 4, 2],
  [5, 6, 3, 2, 1],
  [1, 2, 0, 1, 5],
  [4, 1, 0, 1, 7],
  [1, 0, 3, 0, 5]
]

sumRegion(2, 1, 4, 3) -> 8
sumRegion(1, 1, 2, 2) -> 11
sumRegion(1, 2, 2, 4) -> 12
```
Note:
You may assume that the matrix does not change.
There are many calls to sumRegion function.
You may assume that row1 ≤ row2 and col1 ≤ col2.

### 2.2 Solution
Similar to the 1D version, we can create a matrix to store the region sum for every element with the first element (0, 0) as the left upper corner.

Be careful when calculating the region sum as the overlapped region is added or subtracted twice.

```python
class NumMatrix:

    def __init__(self, matrix):
        """
        :type matrix: List[List[int]]
        """
        self.sum_matrix = matrix
        for row in range(len(matrix)):
            for col in range(len(matrix[0])):
                self.sum_matrix[row][col] += (self.sum_matrix[row - 1][col] if row > 0 else 0) + (self.sum_matrix[row][col - 1] if col > 0 else 0) - (self.sum_matrix[row - 1][col - 1] if row > 0 and col > 0 else 0)
        print(self.sum_matrix)

    def sumRegion(self, row1, col1, row2, col2):
        """
        :type row1: int
        :type col1: int
        :type row2: int
        :type col2: int
        :rtype: int
        """
        if row1 < 0 or col1 < 0 or row2 > len(self.sum_matrix) or col2 > len(self.sum_matrix[0]):
            return 0
        return self.sum_matrix[row2][col2] - (self.sum_matrix[row1 - 1][col2] if row1 > 0 else 0) - (self.sum_matrix[row2][col1 - 1] if col1 > 0 else 0) + (self.sum_matrix[row1 - 1][col1 - 1] if row1 > 0 and col1 > 0 else 0)


# Your NumMatrix object will be instantiated and called as such:
# obj = NumMatrix(matrix)
# param_1 = obj.sumRegion(row1,col1,row2,col2)
```
