### 1. Problem Description
Given n balloons, indexed from 0 to n-1. Each balloon is painted with a number on it represented by array nums. You are asked to burst all the balloons. If the you burst balloon i you will get nums[left] * nums[i] * nums[right] coins. Here left and right are adjacent indices of i. After the burst, the left and right then becomes adjacent.

Find the maximum coins you can collect by bursting the balloons wisely.

Note:
(1) You may imagine nums[-1] = nums[n] = 1. They are not real therefore you can not burst them.
(2) 0 ≤ n ≤ 500, 0 ≤ nums[i] ≤ 100

Example:

Given [3, 1, 5, 8]

Return 167
```
  nums = [3,1,5,8] --> [3,5,8] -->   [3,8]   -->  [8]  --> []
  coins =  3*1*5      +  3*5*8    +  1*3*8      + 1*8*1   = 167
```

### 2. Solutions
##### 2.1 Brute Force
1. Compute coins for every possible combinations
2. Return the maximum

**Error: Time limit exceeded**

```python
class Solution:
    def maxCoins(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        def helper(ava, chosen, coin):
            if not ava:
                coins.append(coin)
            else:
                l = len(ava)
                for i in range(l):
                    this_coin = coin + (ava[i - 1] if i - 1 >= 0 else 1) * ava[i] * (ava[i + 1] if i + 1 < l else 1)
                    helper(ava[:i] + ava[i + 1:], chosen + [ava[i]], this_coin)

        coins = []
        helper(nums, [], 0)

        return max(coins)
```

##### 2.2 DP
The idea is :
1. Add two [i] to the beginning and end of nums

2. Define dp[i][j] to be the maximum coins we can get from the ith to the jth element of nums

3. Define k to be the balloon we choose to burst at last for the section nums[i : j + 1]

4. The final result will be dp[1][n]

**nums**

|i - 1|i|i + 1|...|k - 1|k|k + 1|...|j - 1|j|j + 1
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|||||||||||||

If we reserve the balloon k to burst at last, the coins we get is

```
nums[i - 1] * nums[k] * nums[j + 1]
```

For the left side of nums[k], the maximum is:
```
dp[i][k - 1]
```

For the right side of nums[k], the maximum is:
```
dp[k + 1][j]
```

```
dp[i][j] = max{dp[i][k - 1] + nums[i - 1] * nums[k] * nums[j + 1] + dp[k + 1][j] | i <= k <= j}
```

```python
class Solution:
    def maxCoins(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """

        nums = [1] + [n for n in nums if n > 0] + [1]
        n = len(nums)

        dp = [[0] * n for i in range(n)]

        for l in range(1, n - 1):
            for i in range(1, n - l):
                j = i + l - 1
                for k in range(i, j + 1):
                    dp[i][j] = max(dp[i][j], dp[i][k - 1] + nums[i - 1] * nums[k] * nums[j + 1] + dp[k + 1][j])

        return dp[1][n - 2]
```
