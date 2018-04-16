### 1. Problem Description
Given a positive integer, check whether it has alternating bits: namely, if two adjacent bits will always have different values.

### 2. Solutions
#### 2.1 Solution 1
##### Analysis
Steps:
1. Convert the number into binary representation
2. Iterate over the binary string and compare two char at a time

Runtime:
- T(n) = O(lg(n))

##### Code
```python
class Solution:
    def hasAlternatingBits(self, n):
        """
        :type n: int
        :rtype: bool
        """
        b = bin(n)

        for i in range(2, len(b) - 1):
            if b[i] == b[i + 1]:
                return False
        return True
```

#### 2.2 Solution 2
##### Analysis
Solution 2 is essentially the same as solution 1

Steps:
1. Keep computing the quotients and residuals
2. See if there are two same residuals next to each other

Runtime:
- T(n) = O(lg(n))

##### Code
```python
class Solution:
    def hasAlternatingBits(self, n):
        """
        :type n: int
        :rtype: bool
        """
        quo = n // 2
        res = n % 2

        while quo != 0:
            temp = quo % 2
            if res == temp:
                return False
            res = temp
            quo = quo // 2

        return True
```

#### 2.3 Solution 3
##### Analysis
Steps:
1. Get bitwise n
2. Shift one position to the left or right
3. Do an exclusive or and see if there is '0' in the result

Runtime
- T(n) = O(lg(n))

##### Code
```python
class Solution:
    def hasAlternatingBits(self, n):
        """
        :type n: int
        :rtype: bool
        """
        ans = bin(n ^ (n << 1))
        if '0' in ans[2:-1]:
            return False
        return True
```
