---
layout: default
title: Squares of a Sorted Array
parent: Easy Set 5
grand_parent: DSA Easy
nav_order: 26
permalink: /problem-156-Squares-of-a-Sorted Array/
---
# Squares of a Sorted Array
Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

##### Example 1:
```markdown
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].
```
##### Example 2:
```markdown
Input: nums = [-7,-3,2,3,11]
Output: [4,9,9,49,121]
```
##### Constraints:
* 1 <= nums.length <= 104
* -104 <= nums[i] <= 104
* nums is sorted in non-decreasing order.


Follow up: Squaring each element and sorting the new array is very trivial, could you find an O(n) solution using a different approach?

### Solution:
```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int[] ans = new int[nums.length];
        int s = 0;
        int e = nums.length - 1;
        int i = e;
        
        while(i>=0){
            if(Math.abs(nums[s])>Math.abs(nums[e])) ans[i--] = nums[s]*nums[s++];
            else
                ans[i--] = nums[e]*nums[e--];
        }
        return ans;
    }
}
```