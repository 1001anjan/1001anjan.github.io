---
layout: default
title: Duplicate Zeros
parent: Easy Set 14
grand_parent: DSA Easy
nav_order: 9
permalink: /problem-409-Duplicate Zeros/
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
* 1 <= arr.length <= 10^4
* 0 <= arr[i] <= 9

### Solution:
```java
class Solution {
    public void duplicateZeros(int[] arr) {
        for(int i = 0; i < arr.length - 1; i++){
            if(arr[i] == 0){
                for(int j = arr.length - 2; j > i; j--){
                    arr[j + 1] = arr[j];
                }
                arr[i + 1] = 0;
                i++;
            }
        }
    }
}
```
```java
class Solution {
    public void duplicateZeros(int[] arr) {
        int possibleDups = 0;
        int length_ = arr.length - 1;

        // Find the number of zeros to be duplicated
        // Stopping when left points beyond the last element in the original array
        // which would be part of the modified array
        for (int left = 0; left <= length_ - possibleDups; left++) {

            // Count the zeros
            if (arr[left] == 0) {

                // Edge case: This zero can't be duplicated. We have no more space,
                // as left is pointing to the last element which could be included  
                if (left == length_ - possibleDups) {
                    // For this zero we just copy it without duplication.
                    arr[length_] = 0;
                    length_ -= 1;
                    break;
                }
                possibleDups++;
            }
        }

        // Start backwards from the last element which would be part of new array.
        int last = length_ - possibleDups;

        // Copy zero twice, and non zero once.
        for (int i = last; i >= 0; i--) {
            if (arr[i] == 0) {
                arr[i + possibleDups] = 0;
                possibleDups--;
                arr[i + possibleDups] = 0;
            } else {
                arr[i + possibleDups] = arr[i];
            }
        }
    }
}
```
[Practice link](https://leetcode.com/problems/duplicate-zeros/)