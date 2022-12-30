---
layout: default
title: Mean of Array After Removing Some Elements
parent: Easy Set 8
grand_parent: DSA Easy Difficulty
nav_order: 25
permalink: /problem-245-Mean-of-Array-After-Removing-Some-Elements/
---
# Mean of Array After Removing Some Elements
Given an integer array arr, return the mean of the remaining integers after removing the smallest 5% and the largest 5% of the elements.

Answers within 10-5 of the actual answer will be considered accepted.

##### Example 1:
```markdown
Input: arr = [1,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,3]
Output: 2.00000
Explanation: After erasing the minimum and the maximum values of this array, all elements are equal to 2, so the mean is 2.
```
##### Example 2:
```markdown
Input: arr = [6,2,7,5,1,2,0,3,10,2,5,0,5,5,0,8,7,6,8,0]
Output: 4.00000
```
##### Example 3:
```markdown
Input: arr = [6,0,7,0,7,5,7,8,3,4,0,7,8,1,6,8,1,1,2,4,8,1,9,5,4,3,8,5,10,8,6,6,1,0,6,10,8,2,3,4]
Output: 4.77778
```
##### Constraints:
* 20 <= arr.length <= 1000
* arr.length is a multiple of 20.
* 0 <= arr[i] <= 105

### Solution:
```java
class Solution {
    public double trimMean(int[] arr) {
        Arrays.sort(arr);
        int d = arr.length / 20;
        double sum = 0.0;
        for(int i = d; i < arr.length - d; i++){
            sum += arr[i];
        }
        return sum / (arr.length - 2*d);
    }
}
```