---
layout: default
title: Third Maximum Number
parent: Easy Set 3
grand_parent: DSA Easy Difficulty
nav_order: 13
permalink: /problem-76-Third-Maximum-Number/
---
# Third Maximum Number

Given an integer array nums, return the third distinct maximum number in this array. If the third maximum does not exist, return the maximum number.

##### Example 1:
```markdown
Input: nums = [3,2,1]
Output: 1
Explanation:
The first distinct maximum is 3.
The second distinct maximum is 2.
The third distinct maximum is 1.
```
##### Example 2:
```markdown
Input: nums = [1,2]
Output: 2
Explanation:
The first distinct maximum is 2.
The second distinct maximum is 1.
The third distinct maximum does not exist, so the maximum (2) is returned instead.
```
##### Example 3:
````markdown
Input: nums = [2,2,3,1]
Output: 1
Explanation:
The first distinct maximum is 3.
The second distinct maximum is 2 (both 2's are counted together since they have the same value).
The third distinct maximum is 1.
````
##### Constraints:
* 1 <= nums.length <= 104
* -231 <= nums[i] <= 231 - 1

### Solution:
```java
class Solution {
    public int thirdMax(int[] nums) {
        long max = Long.MIN_VALUE;
        long secondMax = max;
        long thirdMax = secondMax;

        for(int i = 0 ;i<nums.length;i++){
            if(nums[i]>max){
                thirdMax = secondMax;
                secondMax = max;
                max = nums[i];
            }
            else if(nums[i]<max && nums[i]>secondMax){
                thirdMax = secondMax;
                secondMax = nums[i];
            }
            else if(nums[i]<secondMax && nums[i]>thirdMax){
                thirdMax = nums[i];
            }
        }
        return  thirdMax==Long.MIN_VALUE ? (int) max : (int) thirdMax;
    }
}
```