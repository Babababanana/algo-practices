### 1. Problem Description
A matrix is Toeplitz if every diagonal from top-left to bottom-right has the same element.

Now given an M x N matrix, return True if and only if the matrix is Toeplitz.

### 2. Solutions
#### 2.1 Solution 1
##### Analysis
Steps:
1. Get first_col which is the first column of the matrix
2. Get first_row which is the first row of the matrix without matrix[0][0]
3. For each element in first_col, see if element == matrix[i][j], element_idx < i < M, 0 < j < N
4. For each element in first_row, see if element == matrix[i][j], 0 < i < M, element_idx + 1 < j < N

Runtime:
- T(n) = theta(n^2)

##### Code
```python
class Solution:
    def isToeplitzMatrix(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: bool
        """

        n = len(matrix)
        m = len(matrix[0])

        first_col = [matrix[row][0] for row in range(n)]
        first_row = [matrix[0][col] for col in range(1, m)]

        for idx, val in enumerate(first_col):
            i = idx + 1
            j = 1
            while(i < n and j < m):
                if val != matrix[i][j]:
                    return False
                i += 1
                j += 1

        for idx, val in enumerate(first_row):
            i = 1
            j = idx + 2
            while(i < n and j < m):
                if val != matrix[i][j]:
                    return False
                i += 1
                j += 1

        return True
```

#### 2.2 Solution 2
##### Analysis
1. For a 2 x 2 matrix, it is Toeplitz if matrix[0][0] == matrix[1][1]
2. A matrix is Toeplitz if every sub 2 x 2 matrix is Toeplitz

Runtime:
- T = O(M * N)

##### Code
```python
class Solution:
    def isToeplitzMatrix(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: bool
        """
        for row in range(len(matrix) - 1):
            for col in range(len(matrix[0]) - 1):
                if matrix[row][col] != matrix[row + 1][col + 1]:
                    return False
        return True
```
