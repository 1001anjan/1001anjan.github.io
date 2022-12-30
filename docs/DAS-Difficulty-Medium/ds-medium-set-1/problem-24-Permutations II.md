---
layout: default
title: Permutations II
parent: Medium Set 1
grand_parent: DSA Medium Difficulty
nav_order: 24
permalink: /problem-24-Permutations II/
---
# Permutations II
Given a collection of numbers, nums, that might contain duplicates, return all possible unique permutations in any order.

##### Example 1:
```markdown
Input: nums = [1,1,2]
Output:
[[1,1,2],
[1,2,1],
[2,1,1]]
```
##### Example 2:
```markdown
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```
##### Constraints:
* 1 <= nums.length <= 8
* -10 <= nums[i] <= 10

### Solution:
```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(nums);
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

        HashSet<Integer> set = new HashSet<>();

        for(int i = level; i < arr.length; i++){
            if(set.add(arr[i])){
                swap(arr,i,level);
                processPermute(arr, level + 1, ans);
                swap(arr, i, level);
            }
        }
    }

    public void swap(int[] arr, int i, int j){
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```