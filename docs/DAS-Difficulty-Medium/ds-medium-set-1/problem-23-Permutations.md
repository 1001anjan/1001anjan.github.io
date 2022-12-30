---
layout: default
title: Permutations
parent: Medium Set 1
grand_parent: DSA Medium Difficulty
nav_order: 23
permalink: /problem-23-Permutations/
---
# Permutations
Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

##### Example 1:
```markdown
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```
##### Example 2:
```markdown
Input: nums = [0,1]
Output: [[0,1],[1,0]]
```
##### Example 3:
```markdown
Input: nums = [1]
Output: [[1]]
```
##### Constraints:
* 1 <= nums.length <= 6
* -10 <= nums[i] <= 10
* All the integers of nums are unique.

### Solution: 
```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        processPermute(nums,0,ans);
        return ans;
    }

    public void processPermute(int[] arr, int level, List<List<Integer>> ans){
        if(level == arr.length){
            List<Integer> l = new ArrayList<>();
            for(int n : arr) l.add(n);
            ans.add(l);
            return;
        }
           
        for(int i = level; i < arr.length; i++){
            swap(arr,i,level);
            processPermute(arr, level + 1, ans);
            swap(arr,i,level);
        }
    }

    public void swap(int[] arr, int i, int j){
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```