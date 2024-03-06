---
layout: default
title: Find Peak Element
parent: Medium Set 2
grand_parent: DSA Medium
nav_order: 16
permalink: /problem-66-Find Peak Element/
---
# Find Peak Element
A peak element is an element that is strictly greater than its neighbors.

Given a 0-indexed integer array nums, find a peak element, and return its index. If the array contains multiple peaks, return the index to any of the peaks.

You may imagine that nums[-1] = nums[n] = -∞. In other words, an element is always considered to be strictly greater than a neighbor that is outside the array.

You must write an algorithm that runs in O(log n) time.

#####Example 1:
```markdown
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```
##### Example 2:
```markdown
Input: nums = [1,2,1,3,5,6,4]
Output: 5
Explanation: Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.
```
##### Constraints:
* 1 <= nums.length <= 1000
* -2^31 <= nums[i] <= 2^31 - 1
* nums[i] != nums[i + 1] for all valid i.

### Solution:
```java
class Solution {
    public int findPeakElement(int[] nums) {
        if(nums.length == 1) return 0;
        int prev = Integer.MIN_VALUE;
        for(int i = 0; i < nums.length - 1; i++){
            if(nums[i] > prev && nums[i] > nums[i + 1]) return i;
            prev = nums[i];
        }
        if(nums[nums.length - 2] < nums[nums.length - 1]) return nums.length - 1;
        throw null;
    }
}
```
```java
class Solution {
    public int findPeakElement(int[] nums) {
        if (nums == null || nums.length == 1) return 0;
        int start = 0;
        int end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (mid - 1 >= 0 && mid + 1 < nums.length){
                if (nums[mid - 1] < nums[mid] && nums[mid + 1] < nums[mid]) return mid;
                if (nums[mid] < nums[mid - 1]) end = mid;
                else start = mid;
            }   
        }
        if (nums[start] > nums[end]) return start;
        if (nums[end] > nums[start]) return end;
        return 0;
    }
}
```