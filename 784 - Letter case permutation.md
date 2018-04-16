### 1. Problem Description
Given a string S, we can transform every letter individually to be lowercase or uppercase to create another string.  Return a list of all possible strings we could create.

```
Examples:
Input: S = "a1b2"
Output: ["a1b2", "a1B2", "A1b2", "A1B2"]

Input: S = "3z4"
Output: ["3z4", "3Z4"]

Input: S = "12345"
Output: ["12345"]
```

### 2. Solution

##### 2.1 Backtracking
Create a helper function to track the available string and chosen string.

```python
class Solution:
    def letterCasePermutation(self, S):
        """
        :type S: str
        :rtype: List[str]
        """
        def helper(s_ava, s_chosen):
            if s_ava == '':
                res.append(s_chosen)
            else:
                ch = s_ava[0]
                if ch.isalpha():
                    helper(s_ava[1::], s_chosen + ch.lower())
                    helper(s_ava[1::], s_chosen + ch.upper())
                else:
                    helper(s_ava[1::], s_chosen + ch)

        res = []
        helper(S, '')

        return res
```

##### 2.2 List manipulation
All the strings in the res list are prefix for the rest available strings. Create a temp list to hold the prefix combined with the rest strings and assign it back to the res.
```python
res = ['']
for s in S:
    if s.isalpha():
        temp = []
        for pre in res:
            temp.append(pre + s.lower())
            temp.append(pre + s.upper())
        res = temp
    else:
        res = [pre + s for pre in res]

return res
```
