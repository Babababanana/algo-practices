### 1. Problem Description
You are given two arrays (without duplicates) nums1 and nums2 where nums1’s elements are subset of nums2. Find all the next greater numbers for nums1's elements in the corresponding places of nums2.

The Next Greater Number of a number x in nums1 is the first greater number to its right in nums2. If it does not exist, output -1 for this number.

### 2. Solutions
#### 2.1 Solution 1
##### Analysis
If there exists a segment in the list where the elements are in a decreasing order: for example, [3, 2, 1], and the next element is greater than all of them [3, 2, 1, 5], then 5 should be the next greater number for 3, 2, and 1.

Steps:
1.

Runtime:
- T(n) = theta(n)
