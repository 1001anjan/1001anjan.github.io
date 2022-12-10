---
layout: default
title: Subsets
parent: Data Structure Medium Set 1
grand_parent: Data Structure
nav_order: 43
permalink: /problem-43-Subsets/
---
# Subsets
Given an integer array nums of unique elements, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

##### Example 1:
```markdown
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```
##### Example 2:
```markdown
Input: nums = [0]
Output: [[],[0]]
```
##### Constraints:
* 1 <= nums.length <= 10
* -10 <= nums[i] <= 10
* All the numbers of nums are unique.

### Solution:
```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        process(nums, 0, ans, new ArrayList<>());
        return ans;
    }

    public void process(int[] nums, int start, List<List<Integer>> ans, List<Integer> list){
        if(list.size() > nums.length) return;
        ans.add(new ArrayList<>(list));
        for(int i = start; i < nums.length; i++){
            list.add(nums[i]);
            process(nums, i + 1, ans, list);
            list.remove(list.size() - 1);
        }
    }
}
```