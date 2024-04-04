---
layout: default
title: Sum of All Odd Length Subarrays
parent: Easy Set 8
grand_parent: DSA Easy
nav_order: 20
permalink: /problem-240-Sum-of-All-Odd-Length-Subarrays/
---
# Sum of All Odd Length Subarrays
Given an array of positive integers arr, return the sum of all possible odd-length subarrays of arr.

A subarray is a contiguous subsequence of the array.

##### Example 1:
```markdown
Input: arr = [1,4,2,5,3]
Output: 58
Explanation: The odd-length subarrays of arr and their sums are:
[1] = 1
[4] = 4
[2] = 2
[5] = 5
[3] = 3
[1,4,2] = 7
[4,2,5] = 11
[2,5,3] = 10
[1,4,2,5,3] = 15
If we add all these together we get 1 + 4 + 2 + 5 + 3 + 7 + 11 + 10 + 15 = 58
```
##### Example 2:
```markdown
Input: arr = [1,2]
Output: 3
Explanation: There are only 2 subarrays of odd length, [1] and [2]. Their sum is 3.
```
##### Example 3:
```markdown
Input: arr = [10,11,12]
Output: 66
```
##### Constraints:
* 1 <= arr.length <= 100
* 1 <= arr[i] <= 1000

##### Follow up:

Could you solve this problem in O(n) time complexity?

##### Solution:
```java
class Solution {
    public int sumOddLengthSubarrays(int[] arr) {
        int sum = 0;
        for(int i = 0; i < arr.length; i++){
           // calculating no of times index will be present in all subarrays 
            int allCount = (arr.length - i)*(i + 1);
            // calculate no of times index will be present in odd length subarrays
            int oddCount = allCount % 2 == 0 ?  allCount/2 : allCount/2 + 1;
            sum += oddCount*arr[i];
        }
        return sum;
    }
}
```
