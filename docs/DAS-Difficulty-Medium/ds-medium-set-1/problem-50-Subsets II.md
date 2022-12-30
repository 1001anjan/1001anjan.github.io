---
layout: default
title: Subsets II
parent: Medium Set 1
grand_parent: DSA Medium Difficulty
nav_order: 50
permalink: /problem-50-Subsets II/
---
# Subsets II
Given an integer array nums that may contain duplicates, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

##### Example 1:
```markdown
Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
```
##### Example 2:
```markdown
Input: nums = [0]
Output: [[],[0]]
```
##### Constraints:
* 1 <= nums.length <= 10
* -10 <= nums[i] <= 10

### Solution:
```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> ans = new ArrayList<>();
        process(nums, 0, ans, new ArrayList<>());
        return ans;
    }

    public void process(int[] nums, int start, List<List<Integer>> ans, List<Integer> list){
        if(list.size() > nums.length) return;
        ans.add(new ArrayList<>(list));
        for(int i = start; i < nums.length; i++){
            if(i > start && nums[i - 1] == nums[i]) continue;
            list.add(nums[i]);
            process(nums, i + 1, ans, list);
            list.remove(list.size() - 1);
        }
    }
}
```
