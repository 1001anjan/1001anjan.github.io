---
layout: default
title: Contains Duplicate
parent: Easy Set 2
grand_parent: DSA Easy
nav_order: 12
permalink: /problem-43-Contains-Duplicate/
---
# Contains Duplicate

Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

##### Example 1:
```markdown
Input: nums = [1,2,3,1]
Output: true
```
##### Example 2:
```markdown
Input: nums = [1,2,3,4]
Output: false
```
##### Example 3:
```markdown
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
```
##### Constraints:
* 1 <= nums.length <= 105
* -109 <= nums[i] <= 109

### Solution
```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> set = new HashSet();
        for(int i : nums){
            if(set.contains(i)) return true;
            set.add(i);
        }
        return false;
    }
}
```