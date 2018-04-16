# Climbing Stairs
## 1. 746 Climbing Stairs
### 1.1 Problem Description

On a staircase, the i-th step has some non-negative cost cost[i] assigned (0 indexed).

Once you pay the cost, you can either climb one or two steps. You need to find minimum cost to reach the top of the floor, and you can either start from the step with index 0, or the step with index 1.

Example 1:
```
Input: cost = [10, 15, 20]
Output: 15
Explanation: Cheapest is start on cost[1], pay that cost and go to the top.
```
Example 2:
```
Input: cost = [1, 100, 1, 1, 1, 100, 1, 1, 100, 1]
Output: 6
Explanation: Cheapest is start on cost[0], and only step on 1s, skipping cost[3].
```
Note:
cost will have a length in the range [2, 1000].
Every cost[i] will be an integer in the range [0, 999].

### 1.2 Solutions
##### 1.2.1 Bottom-up DP
1. The minimum cost for the ith step is defined by the minimum costs of its two predecessors.

**Optimal Structure**
```
min_cost[i] = cost[i] + min(min_cost[i - 1], min_cost[i - 2])
```

**Recurrence**
```
min_cost[0] = cost[0]
min_cost[1] = cost[1]
min_cost[2] = cost[2] + min(min_cost[0], min_cost[1])
min_cost[3] = cost[3] + min(min_cost[1], min_cost[2])
...
```
**Runtime O(n), Space O(n)**
```python
class Solution:
    def minCostClimbingStairs(self, cost):
        """
        :type cost: List[int]
        :rtype: int
        """
        n = len(cost)

        if n < 2:
            return 0

        dp = [0] * n

        dp[0], dp[1] = cost[0], cost[1]

        for i in range(2, n):
            dp[i] = cost[i] + min(dp[i - 1], dp[i - 2])

        return min(dp[n - 1], dp[n - 2])
```

**Runtime O(n), Space O(1)**
```python
class Solution:
    def minCostClimbingStairs(self, cost):
        """
        :type cost: List[int]
        :rtype: int
        """
        n = len(cost)

        if n < 2:
            return 0

        min_1, min_2 = cost[0], cost[1]

        for i in range(2, n):
            curr_min = cost[i] + min(min_1, min_2)
            min_1 = min_2
            min_2 = curr_min

        return min(min_1, min_2)
```

##### 1.2.2 Recursion
**Base case**
```
min_cost[0] = cost[0]
min_cost[1] = cost[1]
```
**Time limit exceeded**
```python
class Solution:
    def minCostClimbingStairs(self, cost):
        """
        :type cost: List[int]
        :rtype: int
        """        
        def find_min(n):
            if n == 0:
                return cost[0]
            elif n == 1:
                return cost[1]
            else:
                return cost[n] + min(find_min(n - 1), find_min(n - 2))

        l = len(cost)

        if l < 2:
            return 0

        return min(find_min(l - 1), find_min(l - 2))
```

## 2. 70 Climbing Stairs
### 2.1 Problem Description
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.


Example 1:
```
Input: 2
Output:  2
Explanation:  There are two ways to climb to the top.
```
1. 1 step + 1 step
2. 2 steps
Example 2:
```
Input: 3
Output:  3
Explanation:  There are three ways to climb to the top.
```
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
### 2.2 Solutions
This is just a fibonacci problem.
##### 2.2.1 Recursion
**Time limit exceeded**
```python
class Solution:
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n < 2:
            return 1
        else:
            return self.climbStairs(n - 1) + self.climbStairs(n - 2)
```

##### 2.2.2 DP
**Time O(n), Space O(n)**
```python
class Solution:
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """        
        if n < 2:
            return 1

        dp = [0] * (n + 1)
        dp[0] = dp[1] = 1

        for i in range(2, n + 1):
            dp[i] = dp[i - 1] + dp[i - 2]

        return dp[n]
```
**Time O(n), Space O(1)**
```python
class Solution:
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """        
        a = b = 1

        for i in range(n):
            a, b = b, a + b

        return a
```
