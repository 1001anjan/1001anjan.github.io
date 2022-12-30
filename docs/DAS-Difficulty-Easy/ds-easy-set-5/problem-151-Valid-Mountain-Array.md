---
layout: default
title: Valid Mountain Array
parent: Easy Set 5
grand_parent: DSA Easy Difficulty
nav_order: 21
permalink: /problem-151-Valid-Mountain-Array/
---
# Valid Mountain Array

Given an array of integers arr, return true if and only if it is a valid mountain array.

Recall that arr is a mountain array if and only if:

* arr.length >= 3
* There exists some i with 0 < i < arr.length - 1 such that:
  * arr[0] < arr[1] < ... < arr[i - 1] < arr[i]
  * arr[i] > arr[i + 1] > ... > arr[arr.length - 1]


![](../../assets/images/ds/hint_valid_mountain_array.png)
##### Example 1:
```markdown
Input: arr = [2,1]
Output: false
```
##### Example 2:
```markdown
Input: arr = [3,5,5]
Output: false
```
##### Example 3:
```markdown
Input: arr = [0,3,2,1]
Output: true
```
##### Constraints:
* 1 <= arr.length <= 104
* 0 <= arr[i] <= 104

### Solution:
```java
class Solution {
    public boolean validMountainArray(int[] arr) {
        if(arr.length<3) return false;
        int i = 1;
        while(i<arr.length && arr[i-1]<arr[i]) i++;
        if(i == 1 || i == arr.length) return false;
        i--;
        while(i<arr.length-1 && arr[i]>arr[i+1]) i++;
        return i == arr.length-1;
    }
}
```