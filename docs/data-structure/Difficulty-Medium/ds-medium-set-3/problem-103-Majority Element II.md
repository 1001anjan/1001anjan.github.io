---
layout: default
title: Majority Element II
parent: Data Structure Medium Set 3
grand_parent: Data Structure
nav_order: 3
permalink: /problem-103-Majority Element II/
---
# Majority Element II
Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times.

##### Example 1:
```markdown
Input: nums = [3,2,3]
Output: [3]
```
##### Example 2:
```markdown
Input: nums = [1]
Output: [1]
```
##### Example 3:
```markdown
Input: nums = [1,2]
Output: [1,2]
```
##### Constraints:
* 1 <= nums.length <= 5 * 10^4 
* -10^9 <= nums[i] <= 10^9

* Follow up: Could you solve the problem in linear time and in O(1) space?

### Solution:
```java
class Solution {
    public List<Integer> majorityElement(int[] nums) {
        List<Integer> ans = new ArrayList<>();
        Arrays.sort(nums);
        int t = nums.length / 3;
        int c = 1;
        for(int i = 1; i < nums.length; i++){
            if(nums[i - 1] == nums[i]) c++; 
            else{
                if(c > t) ans.add(nums[i - 1]);
                c = 1;
            }
        }
        if(c > t) ans.add(nums[nums.length - 1]);
        return ans;
    }
}
```