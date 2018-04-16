### 1. Problem Description
Given a digit string, return all possible letter combinations that the number could represent.

- Input: str
- Output: List[str]

##### Edge cases
1. Input string length is ""
  - return []
2. If input digit is not any number from 2 - 9
  - there is no letter corresponds to this input digit

### 2. Solution
##### Analysis
This is a combinatorial problem and the result will grow exponentially as the input digit string grows.

##### Code
```python
class Solution:
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        dic = {'2': 'abc', '3': 'def', '4': 'ghi', '5': 'jkl', '6': 'mno', '7': 'pqrs', '8': 'tuv', '9': 'wxyz'}

        result = []

        for digit in digits:
            if digit in dic:
                if result != []:
                    result = [prev + ch for prev in result for ch in dic[digit]]
                else:
                    result = [ch for ch in dic[digit]]

        return result
```
