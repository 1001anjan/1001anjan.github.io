---
layout: default
title: Search Insert Position
parent: Easy Set 1
grand_parent: DSA Easy
nav_order: 10
permalink: /problem-10-search-insert-position/
---
# Search Insert Position
Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with O(log n) runtime complexity.

#### Example 1:
```markdown
Input: nums = [1,3,5,6], target = 5
Output: 2
```
#### Example 2:
```markdown
Input: nums = [1,3,5,6], target = 2
Output: 1
```
#### Example 3:
```markdown
Input: nums = [1,3,5,6], target = 7
Output: 4
```

### Constraints:
* 1 <= nums.length <= 104
* -104 <= nums[i] <= 104
* nums contains distinct values sorted in ascending order.
* -104 <= target <= 104

### Solution
```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        if(nums == null || nums.length == 0)
            return 0;
        
        int i = 0; // start index
        int j = nums.length-1; // last index
        while(i<=j){
            int mid = (i + j)/2; // middle index
            if(nums[mid] == target)
                return mid;       // stop iterating when get target in our array
            else if(nums[mid] < target)
                i = mid + 1;      // goto right-half in array
            else
                j = mid - 1;      // goto left half in array
        }
        return i;
    }
}
```
