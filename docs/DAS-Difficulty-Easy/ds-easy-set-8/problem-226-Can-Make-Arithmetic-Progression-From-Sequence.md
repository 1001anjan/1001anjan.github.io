---
layout: default
title: Can Make Arithmetic Progression From Sequence
parent: Easy Set 8
grand_parent: DSA Easy
nav_order: 6
permalink: /problem-226-Can-Make-Arithmetic-Progression-From-Sequence/
---
# Can Make Arithmetic Progression From Sequence
A sequence of numbers is called an arithmetic progression if the difference between any two consecutive elements is the same.

Given an array of numbers arr, return true if the array can be rearranged to form an arithmetic progression. Otherwise, return false.

##### Example 1:
```markdown
Input: arr = [3,5,1]
Output: true
Explanation: We can reorder the elements as [1,3,5] or [5,3,1] with differences 2 and -2 respectively, between each consecutive elements.
```
##### Example 2:
```markdown
Input: arr = [1,2,4]
Output: false
Explanation: There is no way to reorder the elements to obtain an arithmetic progression.
```
##### Constraints:
* 2 <= arr.length <= 1000
* -106 <= arr[i] <= 106

### Solution:
Time Complexity: O(nLogN)
```java
class Solution {
    public boolean canMakeArithmeticProgression(int[] arr) {
        Arrays.sort(arr);
        int diff = arr[0] - arr[1];
        for(int i = 1; i < arr.length - 1; i++){
            if(diff != arr[i] - arr[i + 1]) return false;
        }
        return true;
    }
}
```
