---
layout: default
title: Combination Sum II
parent: Medium Set 1
grand_parent: DSA Medium Difficulty
nav_order: 21
permalink: /problem-21-Combination Sum II/
---
# Combination Sum II
Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target.

Each number in candidates may only be used once in the combination.

Note: The solution set must not contain duplicate combinations.

##### Example 1:
```markdown
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output:
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
```
##### Example 2:
```markdown
Input: candidates = [2,5,2,1,2], target = 5
Output:
[
[1,2,2],
[5]
]
```
##### Constraints:
* 1 <= candidates.length <= 100
* 1 <= candidates[i] <= 50
* 1 <= target <= 30

### Solution: 
```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(candidates);
        process(0, candidates, target, ans, new ArrayList<Integer>());
        return ans;   
    }

    public void process(int start, int[] arr, int target, List<List<Integer>> ans, List<Integer> list){
        
        if(target == 0) {
            ans.add(new ArrayList<>(list));
            return;
        }
    
        for(int i = start; i < arr.length; i++){
            if(i > start && arr[i] == arr[i - 1]){
                continue;
            }
            if(target >= arr[i]){
                list.add(arr[i]);
                process(i + 1,arr,target - arr[i],ans,list);
                list.remove(list.size() - 1);
            }
        }
    }
}
```