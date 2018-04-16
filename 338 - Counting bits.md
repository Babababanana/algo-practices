### 1. Problem Description
Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

Example:
```
For num = 5 you should return [0,1,1,2,1,2].
```

Follow up:

It is very easy to come up with a solution with run time O(n*sizeof(integer)). But can you do it in linear time O(n) /possibly in a single pass?
Space complexity should be O(n).
Can you do it like a boss? Do it without using any builtin function like ```__builtin_popcount``` in c++ or in any other language.

### 2. Solutions
##### 2.1 Trivial way
```python
class Solution(object):
    def countBits(self, num):
        """
        :type num: int
        :rtype: List[int]
        """
        res = []

        for i in range(num + 1):
            res.append(bin(i).count('1'))
        return res
```

##### 2.2 DP
If a number is the power of 2, the number of 1 is 1.
**Optimal Structure**
```
dp[0] = 0
dp[1] = 1
dp[2] = 1
dp[3] = 2
dp[4] = 1
dp[5] = 2
dp[6] = 2
dp[7] = 3
dp[8] = 1
...
```
```
0 ~ 1:    01    nearest base 2 ^ 0 = 1
2 ~ 3:    12    nearest base 2 ^ 1 = 2
4 ~ 7:    1223  nearest base 2 ^ 2 = 4
8 ~ 11:   1223  nearest base 2 ^ 3 = 8
12 ~ 15:  2334  nearest base 2 ^ 3 = 8
16 ~ 19:  1223  nearest base 2 ^ 4 = 16
20 ~ 23:  2334  nearest base 2 ^ 4 = 16
24 ~ 27:  2334  nearest base 2 ^ 4 = 16
28 ~ 31:  3445  nearest base 2 ^ 4 = 16
...
```
The pattern is
```
dp[index] = 1 + dp[index - nearest]
```

```python
class Solution:
    def _is_powerof2(self, num):
        return (num & (num - 1)) == 0
    def countBits(self, num):
        """
        :type num: int
        :rtype: List[int]
        """
        if num < 1:
            return [0]

        dp = [0, 1]

        nearest = 0

        for i in range(2, num + 1):
            if self._is_powerof2(i):
                nearest = i
            dp.append(1 + dp[i - nearest])

        return dp
```
