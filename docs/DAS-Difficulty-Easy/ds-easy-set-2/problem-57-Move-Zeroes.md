---
layout: default
title: Move Zeroes
parent: Easy Set 2
grand_parent: DSA Easy Difficulty
nav_order: 26
permalink: /problem-57-Move-Zeroes/
---
# Move Zeroes

Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.

##### Example 1:
```markdown
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]
```
##### Example 2:
```markdown
Input: nums = [0]
Output: [0]
```
##### Constraints:
* 1 <= nums.length <= 104
* -231 <= nums[i] <= 231 - 1

### Solution
##### Faster 
```java
class Solution {
    public void moveZeroes(int[] nums) {        
        int cnt = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != 0) {
                if (i > cnt) {
                    nums[cnt] = nums[i];                    
                }
                cnt++;
            }
        }
        while (cnt < nums.length) {
            nums[cnt++] = 0;
        }
    }
}
```
```java
class Solution {
    public void moveZeroes(int[] nums) {
        int i = 0;
        int j = 0;
        int temp;
        while(i<nums.length && j<nums.length){
            while(i<nums.length && nums[i] != 0) i++;
            j = i;
            while(j<nums.length && nums[j] == 0) j++;
            if(i<nums.length && j<nums.length){
                nums[i] = nums[j];
                nums[j] = 0;
            }
            i++;
        }
        
    }
}
```
##### without maintaining order
```java
class Solution {
    public void moveZeroes(int[] nums) {
        int i = 0;
        int j = nums.length - 1;
        int temp;
        while(i<j){
            while(i<=j && nums[i] != 0) i++;
            while(j>=0 && nums[j] == 0) j--;
            if(i<nums.length-1 && j>=0){
                temp = nums[i];
                nums[i] = nums[j];
                nums[j] = temp;
                i++;
                j--;
            }
            
        }
    }
}
```
