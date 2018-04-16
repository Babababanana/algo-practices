### 1. Problem Description
A self-dividing number is a number that is divisible by every digit it contains.

For example, 128 is a self-dividing number because 128 % 1 == 0, 128 % 2 == 0, and 128 % 8 == 0.

Also, a self-dividing number is not allowed to contain the digit zero.

Given a lower and upper number bound, output a list of every possible self dividing number, including the bounds if possible.

- Input: left - int, right - int
- Output: List[int]

##### Edge cases
1. left == right
 - return []

### 3. Solution
##### Analysis
Steps:
1. Iterate over range(left, right + 1)
2. Convert number to string
3. Find if it contains '0'
4. Find if it is self-dividable

Runtime:
- T = O(n)

##### Code
```python
class Solution:
    def selfDividingNumbers(self, left, right):
        """
        :type left: int
        :type right: int
        :rtype: List[int]
        """
        if left == right:
            return []
        result = []
        for num in range(left, right + 1):
            s = str(num)
            if '0' in s:
                continue

            self_div = True
            for d in s:
                if num % int(d) != 0:
                    self_div = False

            if self_div:
                result.append(num)

        return result
```
