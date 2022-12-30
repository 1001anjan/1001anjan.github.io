---
layout: default
title: Duplicate Zeros
parent: Easy Set 6
grand_parent: DSA Easy Difficulty
nav_order: 22
permalink: /problem-182-Duplicate-Zeros/
---
# Duplicate Zeros

Given a fixed-length integer array arr, duplicate each occurrence of zero, shifting the remaining elements to the right.

Note that elements beyond the length of the original array are not written. Do the above modifications to the input array in place and do not return anything.

##### Example 1:
```markdown
Input: arr = [1,0,2,3,0,4,5,0]
Output: [1,0,0,2,3,0,0,4]
Explanation: After calling your function, the input array is modified to: [1,0,0,2,3,0,0,4]
```
##### Example 2:
```markdown
Input: arr = [1,2,3]
Output: [1,2,3]
Explanation: After calling your function, the input array is modified to: [1,2,3]
```
##### Constraints:
* 1 <= arr.length <= 104
* 0 <= arr[i] <= 9

### Solution:
