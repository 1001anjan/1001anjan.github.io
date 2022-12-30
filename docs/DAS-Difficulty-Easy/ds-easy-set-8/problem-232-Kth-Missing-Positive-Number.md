---
layout: default
title: Kth Missing Positive Number
parent: Easy Set 8
grand_parent: DSA Easy Difficulty
nav_order: 12
permalink: /problem-232-Kth-Missing-Positive-Number/
---
# Kth Missing Positive Number

Given an array arr of positive integers sorted in a strictly increasing order, and an integer k.

Return the kth positive integer that is missing from this array.

##### Example 1:
```markdown
Input: arr = [2,3,4,7,11], k = 5
Output: 9
Explanation: The missing positive integers are [1,5,6,8,9,10,12,13,...]. The 5th missing positive integer is 9.
```
##### Example 2:
```markdown
Input: arr = [1,2,3,4], k = 2
Output: 6
Explanation: The missing positive integers are [5,6,7,...]. The 2nd missing positive integer is 6.
```
##### Constraints:
* 1 <= arr.length <= 1000
* 1 <= arr[i] <= 1000
* 1 <= k <= 1000
* arr[i] < arr[j] for 1 <= i < j <= arr.length

##### Follow up:

Could you solve this problem in less than O(n) complexity?

### Solution
```java
class Solution {
    public int findKthPositive(int[] arr, int k) {
        int count = 0;
        int i = 1;
        int j = 0;
        while(count != k){
            if(j < arr.length && arr[j] == i){
                j++;
            }else{
                count++;
            }
            i++;
        }
        return i-1;
    }
}
```