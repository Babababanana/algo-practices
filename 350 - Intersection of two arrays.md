### 1. Problem Description
Given two arrays, write a function to compute their intersection.

Example:
```
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2, 2].
```

Note:
Each element in the result should appear as many times as it shows in both arrays.
The result can be in any order.

Follow up:<br/>
What if the given array is already sorted? How would you optimize your algorithm?
What if nums1's size is small compared to nums2's size? Which algorithm is better?
What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

### 2. Solutions
##### 2.1 Brute Force (192ms)

**Runtime: O(n^2), Space: O(n)**

```python
class Solution:
    def intersect(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        inter = {}

        for i in range(len(nums2)):
            for j in range(len(nums1)):
                if nums2[i] == nums1[j] and j not in inter:
                    inter[j] = nums1[j]
                    break

        return [val for val in inter.values()]
```
##### 2.2 Brute Force + Binary Search (52ms)

**Runtime: O(n*logn), Space: O(n)**

```python
class Solution:
    def intersect(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """        
        inter = []
        nums1.sort()

        for num in nums2:
            if not nums1:
                break
            loc = self.binary_search(num, nums1)
            if loc > -1:
                inter.append(nums1.pop(loc))

        return inter

    def binary_search(self, num, arr):
        low = 0
        high = len(arr) - 1

        if num > arr[-1] or num < arr[0]:
            return -1

        while(low <= high):
            mid = (low + high) // 2

            if arr[mid] > num:
                high = mid - 1
            elif arr[mid] < num:
                low = mid + 1
            else:
                return mid
        return -1
```

Runtime with and without the following line are 52ms and 92ms
```python
if num > arr[-1] or num < arr[0]:
    return -1
```

##### 2.3 Dictionary (84ms)
1. Iterate through nums1 and count the appearances of each number
2. Iterate through nums2 and find if each item is in the count dictionary and its count > 0

**Runtime: O(m + n), Space: O(n)**

```python
class Solution:
    def intersect(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """        
        count = {}
        res = []

        for num in nums1:
            count[num] = count[num] + 1 if num in count else 1

        for num in nums2:
            if num in count and count[num] > 0:
                res.append(num)
                count[num] -= 1

        return res
```

##### 2.4 Sort + Pointers (44ms)
1. Sort the two arrays
2. Two pointers start from 0 and scan the two arrays

**Runtime: O(n), Space: O(n)**

```python
class Solution:
    def intersect(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """        
        res = []

        p1 = p2 = 0
        nums1.sort()
        nums2.sort()

        while p1 < len(nums1) and p2 < len(nums2):
            if nums1[p1] < nums2[p2]:
                p1 += 1
            elif nums1[p1] > nums2[p2]:
                p2 += 1
            else:
                res.append(nums1[p1])
                p1 += 1
                p2 += 1
        return res
```

##### 3rd follow up question
In general, we want to minimize the number of disk access.

**Solution 1:** <br/>
1. Sort nums2 using external sort
2. Read and operate them in chunks which fit into the memory limit
3. Repeat until no more data to read from disk.

**Solution 2:** <br/>
1. Store the two arrays in distributed system
2. Use MapReduce to solve the problem
