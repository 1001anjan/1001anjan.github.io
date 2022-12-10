---
layout: default
title: Partition-Array-Into-Three-Parts-With-Equal-Sum
parent: Data Structure Easy Set 6
grand_parent: Data Structure
nav_order: 3
permalink: /problem-161-Partition-Array-Into-Three-Parts-With-Equal-Sum/
---
# Partition Array Into Three Parts With Equal Sum
Given an array of integers arr, return true if we can partition the array into three non-empty parts with equal sums.

Formally, we can partition the array if we can find indexes i + 1 < j with (arr[0] + arr[1] + ... + arr[i] == arr[i + 1] + arr[i + 2] + ... + arr[j - 1] == arr[j] + arr[j + 1] + ... + arr[arr.length - 1])

##### Example 1:
```markdown
Input: arr = [0,2,1,-6,6,-7,9,1,2,0,1]
Output: true
Explanation: 0 + 2 + 1 = -6 + 6 - 7 + 9 + 1 = 2 + 0 + 1
```
##### Example 2:
```markdown
Input: arr = [0,2,1,-6,6,7,9,-1,2,0,1]
Output: false
```
##### Example 3:
```markdown
Input: arr = [3,3,6,5,-2,2,5,1,-9,4]
Output: true
Explanation: 3 + 3 = 6 = 5 - 2 + 2 + 5 + 1 - 9 + 4
```
##### Constraints:
* 3 <= arr.length <= 5 * 104
* -104 <= arr[i] <= 104

### Solution:
```java
class Solution {
    public boolean canThreePartsEqualSum(int[] arr) {
        int sum = 0;
        for(int n : arr) sum += n;
        if(sum % 3 != 0) return false;
        int parts = sum/3;
        int count  = 0;
        sum = 0;
        for(int i=0; i<arr.length; i++){
            sum += arr[i];
            if(sum == parts){
                count ++;
                sum = 0;
            }
        }
        return count >= 3;
    }
}
```