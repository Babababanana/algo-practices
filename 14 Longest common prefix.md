### 1. Problem Description
Write a function to find the longest common prefix string amongst an array of strings.

- Input: List[str]
- Output: str

##### Edge cases
1. List length is 0
  - return ''
2. List length is 1
  - return List[0]

### 2. Solutions
#### 2.1 Solution 1
##### Analysis
1. Find the common prefix string of two strings
2. Always keep the shortest prefix
3. Keep the shorter string of the two and compare it with next string in the list

##### Code
```python
class Solution:
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        if len(strs) < 1:
            return ''

        shorter_str = strs[0]
        shorter_prefix = strs[0]

        for i in range(1, len(strs)):
            j = 0
            prefix = ''
            while j < len(shorter_str) and j < len(strs[i]):
                if shorter_str[j] == strs[i][j]:
                    prefix += shorter_str[j]
                    j += 1
                else:
                    break
            if shorter_prefix > prefix:
                shorter_prefix = prefix

            if strs[i] < shorter_str:
                shorter_str = strs[i]

        return shorter_prefix
```
#### 2.2 Solution 2 (from leetcode)
##### Analysis
A common prefix for a list of strings must exist in every item of the list.

##### Code
```python
class Solution:
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        # return '' if strs is empty
        if not strs:
            return ''
        # unpack strs
        # zip them into a list of tuples
        # iterate over the list
        for i, chars in enumerate(zip(*strs)):
            # if the set of chars contains more than 1 element
            if len(set(chars)) > 1:
              # return the prefix of the first string to the index of i
              return strs[0][:i]
        # return the shortest item in strs
        return min(strs)
```

### 3. Lessons learned
1. ```*``` is an unpacking operator
```python
p = [[1,2,3], [4,5,6]]
>>> *p
[1,2,3],[4,5,6]
```

2. ```zip(iterable,...)``` returns a list of tuples, where the i-th tuple contains the i-th element from each of the argument sequences or iterables.
```python
>>> zip(*p)
[(1,4), (2,5), (3,6)]
```
The number of tuples in the zipped result will be equivalent to the length of the shortest element of the iterables

3. ```enumerate(sequence, start=0)``` Return an enumerate object contains item index and item. sequence must be a sequence, an iterator, or some other object which supports iteration.
```python
>>> seasons = ['Spring', 'Summer', 'Fall', 'Winter']
>>> list(enumerate(seasons))
[(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
>>> list(enumerate(seasons, start=1))
[(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
```
