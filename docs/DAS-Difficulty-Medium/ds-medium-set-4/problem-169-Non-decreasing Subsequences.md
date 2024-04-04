---
layout: default
title: Non-decreasing Subsequences
parent: Medium Set 4
grand_parent: DSA Medium
nav_order: 19
permalink: /problem-169-Non-decreasing Subsequences/
---
# Non-decreasing Subsequences
Given an integer array nums, return all the different possible non-decreasing subsequences of the given array with at least two elements. You may return the answer in any order.

##### Example 1:
```markdown
Input: nums = [4,6,7,7]
Output: [[4,6],[4,6,7],[4,6,7,7],[4,7],[4,7,7],[6,7],[6,7,7],[7,7]]
```
##### Example 2:
```markdown
Input: nums = [4,4,3,2,1]
Output: [[4,4]]
```
##### Constraints:
* 1 <= nums.length <= 15
* -100 <= nums[i] <= 100

### Solution:
```java
class Solution {
    public List<List<Integer>> findSubsequences(int[] nums) {
        Set<List<Integer>> ans = new HashSet<>();
        for(int i = 0; i < nums.length - 1; i++){
            processSubsequences(i, nums, ans, new ArrayList<>());
        }

        return new ArrayList<>(ans);
    }

    private void processSubsequences(int start, int[] nums, Set<List<Integer>> ans, List<Integer> list){
        list.add(nums[start]);
        if(list.size() > 1){
            ans.add(new ArrayList<>(list));
        }
        for(int i = start + 1; i < nums.length; i++){
            if(nums[start] <= nums[i]){
                processSubsequences(i, nums, ans, list);
                list.remove(list.size() - 1);
            }
        }
    }
}
```
##### Complexity Analysis: 
The total number of subsequences (including the empty one) of an array numsnumsnums is 2^n. In the worst case, we may check all of them.

* Time Complexity: O(2^n * n)
* Space Complexity: O(2^n)