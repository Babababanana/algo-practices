### 1. Problem Description
Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

Example 1:
```
Input: 121
Output: true
```
Example 2:
```
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```
Example 3:
```
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

Follow up: Could you solve it without converting the integer to a string?

### 2. Solutions
#### 2.1 Solution 1
Convert integer to string
##### Analysis
Steps:
1. Convert integer to string
2. See if the string and its reversion are the same

##### Code
1. Python (296 ms)
```python
class Solution:
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        str_x = str(x)
        return str_x == str_x[::-1]
```

2. Java (301 ms)
```java
class Solution {
    public boolean isPalindrome(int x) {
        String str = Integer.toString(x);

        String rev = new StringBuffer(str).reverse().toString();

        return str.equals(rev);
    }
}
```

#### 2.2 Solution 2
##### Analysis
Steps:
1. Convert integer to chars
2. Use two pointers at the beginning and end see if the chars are equal.

##### Code
1. Python (284 ms)
```python
class Solution:
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        str_x = str(x)
        i, j = 0, len(str_x) - 1

        while i < j:
            if str_x[i] != str_x[j]:
                return False
            i += 1
            j -= 1
        return True
```
2. Java (282 ms)
```java
class Solution {
    public boolean isPalindrome(int x) {
        char chs[] = Integer.toString(x).toCharArray();

        int i = 0;
        int j = chs.length - 1;

        while(i < j){
            if(chs[i] != chs[j])
                return false;
            i++;
            j--;
        }
        return true;
    }
}
```
#### 2.3 Solution 3
Without converting to string
##### Analysis
Steps:
1. Calculate reversed number while using x % 10
2. Return if the reversed number is equal to the original
##### Code
1. Python (300 ms)
```python
class Solution:
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        if x < 0 or (x % 10 == 0 and x // 10 != 0):
            return False

        n = x
        rev = 0

        while n != 0:
            rev = rev * 10 + n % 10
            n = n // 10
        return rev == x
```
2. Java (211 ms)
```java
class Solution {
    public boolean isPalindrome(int x) {
        if(x < 0 || (x % 10 == 0 && x / 10 != 0))
            return false;

        int n = x;
        int rev = 0;

        while(n != 0){
            rev = rev * 10 + n % 10;
            n /= 10;
        }
        return rev == x;
    }
}
```























```
