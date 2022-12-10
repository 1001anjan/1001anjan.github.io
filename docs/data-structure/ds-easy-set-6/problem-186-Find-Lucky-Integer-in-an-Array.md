---
layout: default
title: Find Lucky Integer in an Array
parent: Data Structure Easy Set 6
grand_parent: Data Structure
nav_order: 26
permalink: /problem-186-Find-Lucky-Integer-in-an-Array/
---
# Find Lucky Integer in an Array

Given an array of integers arr, a lucky integer is an integer that has a frequency in the array equal to its value.

Return the largest lucky integer in the array. If there is no lucky integer return -1.

##### Example 1:
```markdown
Input: arr = [2,2,3,4]
Output: 2
Explanation: The only lucky number in the array is 2 because frequency[2] == 2.
```
##### Example 2:
```markdown
Input: arr = [1,2,2,3,3,3]
Output: 3
Explanation: 1, 2 and 3 are all lucky numbers, return the largest of them.
```
##### Example 3:
```markdown
Input: arr = [2,2,2,3,3]
Output: -1
Explanation: There are no lucky numbers in the array.
```
##### Constraints:
* 1 <= arr.length <= 500
* 1 <= arr[i] <= 500

### Solution:
```java
class Solution {
    public int findLucky(int[] arr) {
        int [] count = new int[501];
        for(int n : arr) count[n]++;
        for(int i = 500; i>=1; i--){
            if(i == count[i]) return i;
        }
        return -1;
    }
}
```