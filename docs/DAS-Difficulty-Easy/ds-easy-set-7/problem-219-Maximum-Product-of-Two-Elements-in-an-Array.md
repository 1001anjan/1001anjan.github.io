---
layout: default
title: Maximum Product of Two Elements in an Array
parent: Easy Set 7
grand_parent: DSA Easy Difficulty
nav_order: 29
permalink: /problem-219-Maximum-Product-of-Two-Elements-in-an-Array/
---
# Maximum Product of Two Elements in an Array
Given the array of integers nums, you will choose two different indices i and j of that array. Return the maximum value of (nums[i]-1)*(nums[j]-1).

##### Example 1:
```markdown
Input: nums = [3,4,5,2]
Output: 12
Explanation: If you choose the indices i=1 and j=2 (indexed from 0), you will get the maximum value, that is, (nums[1]-1)*(nums[2]-1) = (4-1)*(5-1) = 3*4 = 12.
```
##### Example 2:
```markdown
Input: nums = [1,5,4,5]
Output: 16
Explanation: Choosing the indices i=1 and j=3 (indexed from 0), you will get the maximum value of (5-1)*(5-1) = 16.
```
##### Example 3:
```markdown
Input: nums = [3,7]
Output: 12
```
##### Constraints:
* 2 <= nums.length <= 500
* 1 <= nums[i] <= 10^3

### Solution:
```java
class Solution {
    public int maxProduct(int[] nums) {
        int max1, max2;
        if(nums[0] > nums[1]){
            max1 = nums[0];
            max2 = nums[1];
        }else{
            max1 = nums[1];
            max2 = nums[0];
        }
        
        for(int i = 2; i < nums.length; i++){
            if(max1 < nums[i]){
                max2 = max1;
                max1 = nums[i];
            }else if(max2 < nums[i]){
                max2 = nums[i];
            }
        }
        
        return (max1 - 1)*(max2 - 1);
    }
}
```