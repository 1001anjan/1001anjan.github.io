---
layout: default
title: Element Appearing More Than 25% In Sorted Array
parent: Data Structure Easy Set 6
grand_parent: Data Structure
nav_order: 30
permalink: /problem-190-Element-Appearing-More-Than-25%-In-Sorted-Array/
---
# Element Appearing More Than 25% In Sorted Array
Given an integer array sorted in non-decreasing order, there is exactly one integer in the array that occurs more than 25% of the time, return that integer.

##### Example 1:
```markdown
Input: arr = [1,2,2,6,6,6,6,7,10]
Output: 6
```
##### Example 2:
```markdown
Input: arr = [1,1]
Output: 1
```
##### Constraints:
* 1 <= arr.length <= 104
* 0 <= arr[i] <= 105

### Solution:
```java
class Solution {
    public int findSpecialInteger(int[] arr) {
        int currSum = 1;
        for(int i = 1; i < arr.length; i++){
            if(arr[i-1] == arr[i]) 
                currSum ++;
            else{
                if(currSum > arr.length/4) return arr[i-1];
                currSum = 1;
            }
        }
        if(currSum > arr.length/4) return arr[arr.length-1];
        throw null;
    }
}
```