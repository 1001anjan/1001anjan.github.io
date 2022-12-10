---
layout: default
title: Sort Colors
parent: Data Structure Medium Set 1
grand_parent: Data Structure
nav_order: 41
permalink: /problem-41-Sort Colors/
---
# Sort Colors
Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

##### Example 1:
```markdown
Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```
##### Example 2:
```markdown
Input: nums = [2,0,1]
Output: [0,1,2]
```
##### Constraints:
* n == nums.length
* 1 <= n <= 300
* nums[i] is either 0, 1, or 2.

Follow up: Could you come up with a one-pass algorithm using only constant extra space?

### Solution:
```java
class Solution {
    public void sortColors(int[] nums) {
        int s = 0,e = 0; 
        int l = nums.length - 1; 
        int pivot = 1;
        while(e <= l){
            if(nums[e] < pivot){
                swap(nums, s, e);
                s++;
                e++;
            }
            else if(nums[e] == pivot){
                e++;
            }
            else{
                swap(nums, e, l);
                l--;
            }
        
        }
    }

    public void swap(int[] arr, int i, int j){
        int t = arr[i];
        arr[i] = arr[j];
        arr[j] = t;
    }
}
```