---
layout: default
title: Combination Sum
parent: Medium Set 1
grand_parent: DSA Medium
nav_order: 20
permalink: /problem-20-Combination Sum/
---
# Combination Sum
Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order.

The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the
frequency
of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to target is less than 150 combinations for the given input.

##### Example 1:
```markdown
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
```
##### Example 2:
```markdown
Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]
```
##### Example 3:
```markdown
Input: candidates = [2], target = 1
Output: []
```
##### Constraints:
* 1 <= candidates.length <= 30
* 2 <= candidates[i] <= 40
* All elements of candidates are distinct.
* 1 <= target <= 40

### Solution:
```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(candidates);
        for(int i = 0; i < candidates.length; i++){
            process(candidates, i, candidates.length - 1, target - candidates[i],
                    ans, new ArrayList<Integer>(Arrays.asList(candidates[i])));
        }

        return ans;
    }


    public void process(int[] arr, int currentIndex, int searchIndex, int target, List<List<Integer>> list, List<Integer> elist){
        if(searchIndex < 0) return;
        if(target == 0){
            list.add(elist);
        }
        for(int i = searchIndex; i >= currentIndex; i--){
            if(target == arr[i]){
                List<Integer> l = new ArrayList<>(elist);
                l.add(arr[i]);
                list.add(l);
            }
            if(target > arr[i]){
                List<Integer> l = new ArrayList<>(elist);
                l.add(arr[i]);
                process(arr,currentIndex, i,target - arr[i], list,l);
            }
        }

    }
}
```
```java
public class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        //special case
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if(candidates == null || candidates.length == 0)
            return res;
        Arrays.sort(candidates);
        help(res, new ArrayList<Integer>(), target, 0, candidates);
        return res;
    }
    
    public void help(List<List<Integer>> res, ArrayList<Integer> tmp, int target, int start, int [] candidates)
    {
        if(target == 0)
        {
            res.add(new ArrayList<Integer> (tmp));
            return;
        }
        else
        {
            for(int i = start;i<candidates.length;i++)
            {
                if(i > start && candidates[i] == candidates[i-1])
                    continue;
                if(target >= candidates[i])
                {
                    tmp.add(new Integer(candidates[i]));
                    help(res, tmp, target - candidates[i],i,candidates);
                    tmp.remove(tmp.size()-1);
                }
            }
        }
    }
}
```