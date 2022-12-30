---
layout: default
title: Find Minimum in Rotated Sorted Array
parent: Medium Set 2
grand_parent: DSA Medium Difficulty
nav_order: 22
permalink: /problem-72-Find Minimum in Rotated Sorted Array/
---
# Find Minimum in Rotated Sorted Array
Suppose an array of length n sorted in ascending order is rotated between 1 and n times. For example, the array nums = [0,1,2,4,5,6,7] might become:

* [4,5,6,7,0,1,2] if it was rotated 4 times.
* [0,1,2,4,5,6,7] if it was rotated 7 times.
* Notice that rotating an array [a[0], a[1], a[2], ..., a[n-1]] 1 time results in the array [a[n-1], a[0], a[1], a[2], ..., a[n-2]].

Given the sorted rotated array nums of unique elements, return the minimum element of this array.

You must write an algorithm that runs in O(log n) time.

##### Example 1:
```markdown
Input: nums = [3,4,5,1,2]
Output: 1
Explanation: The original array was [1,2,3,4,5] rotated 3 times.
```
##### Example 2:
```markdown
Input: nums = [4,5,6,7,0,1,2]
Output: 0
Explanation: The original array was [0,1,2,4,5,6,7] and it was rotated 4 times.
```
##### Example 3:
```markdown
Input: nums = [11,13,15,17]
Output: 11
Explanation: The original array was [11,13,15,17] and it was rotated 4 times.
```
##### Constraints:
* n == nums.length
* 1 <= n <= 5000
* -5000 <= nums[i] <= 5000
* All the integers of nums are unique.
* nums is sorted and rotated between 1 and n times.

### Solution:
```java
class Solution {
    public int findMin(int[] nums) {

        int s = 0, e = nums.length - 1;
        if(nums.length == 2) return nums[0] < nums[1]? nums[0] : nums[1];
        while(s <= e){
            if(e - s == 1) return nums[s] < nums[e]? nums[s] : nums[e];
            int mid = (s + e)/2;
            if(s == e) return nums[s];
            if(mid == 0 || mid == nums.length - 1) return nums[mid];
            if(nums[mid] < nums[mid - 1] && nums[mid] < nums[mid + 1]) return nums[mid];
            if(nums[s] > nums[e]){
                if(nums[mid] > nums[s] && nums[mid] > nums[e]){
                    s = mid + 1;
                }else{
                    e = mid - -1;
                }
            }else{
                if(nums[mid] > nums[s] && nums[mid] < nums[e]){
                    e = mid - 1;
                }else{
                    s = mid + 1;
                }
            }
        }
        throw null;
    }
}
```
```java
class Solution {
    public int findMin(int[] nums) {
        int lo = 0, hi = nums.length - 1;
        while (lo < hi) {
            int mid = (lo + hi) / 2;
                
            if (nums[mid] < nums[hi]) {
                hi = mid;    
            } else {
                lo = mid + 1; 
            }
        }
        return nums[lo];
    }
}
```