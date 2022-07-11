---
layout: default
title: Contains Duplicate II
parent: Data Structure Easy Set 2
grand_parent: Data Structure
nav_order: 13
permalink: /problem-44-Contains-Duplicate-II/
---
# Contains Duplicate II
Given an integer array nums and an integer k, return true if there are two distinct indices i and j in the array such that nums[i] == nums[j] and abs(i - j) <= k.

##### Example 1:
```markdown
Input: nums = [1,2,3,1], k = 3
Output: true
```
##### Example 2:
```markdown
Input: nums = [1,0,1,1], k = 1
Output: true
```
##### Example 3:
```markdown
Input: nums = [1,2,3,1,2,3], k = 2
Output: false
```
##### Constraints:

* 1 <= nums.length <= 105
* -109 <= nums[i] <= 109
* 0 <= k <= 105

### Solution
```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        for(int i = 0; i<nums.length; i++){
            if(map.containsKey(nums[i])){
                if(Math.abs(map.get(nums[i]) - i) <= k) return true;
            }
            map.put(nums[i],i);
        }
        return false;
    }
}
```