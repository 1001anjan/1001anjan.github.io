---
layout: default
title: Intersection of Multiple Arrays
parent: Easy Set 12
grand_parent: DSA Easy
nav_order: 10
permalink: /problem-350-Intersection of Multiple Arrays/
---
# Intersection of Multiple Arrays
Given a 2D integer array nums where nums[i] is a non-empty array of distinct positive integers, return the list of integers that are present in each array of nums sorted in ascending order.

##### Example 1:
```markdown
Input: nums = [[3,1,2,4,5],[1,2,3,4],[3,4,5,6]]
Output: [3,4]
Explanation:
The only integers present in each of nums[0] = [3,1,2,4,5], nums[1] = [1,2,3,4], and nums[2] = [3,4,5,6] are 3 and 4, so we return [3,4].
```
##### Example 2:
```markdown
Input: nums = [[1,2,3],[4,5,6]]
Output: []
Explanation:
There does not exist any integer present both in nums[0] and nums[1], so we return an empty list [].
```
##### Constraints:
* 1 <= nums.length <= 1000
* 1 <= sum(nums[i].length) <= 1000
* 1 <= nums[i][j] <= 1000
* All the values of nums[i] are unique.

### Solution:
```java
class Solution {
    public List<Integer> intersection(int[][] nums) {
        int[] dp = new int[1001];
        for(int[] arr : nums){
            for(int n : arr) dp[n]++;
        }
        List<Integer> ans = new LinkedList();
        for(int i = 0; i < 1001; i++){
            if(dp[i] == nums.length) ans.add(i);
        }
        
        return ans;
    }
}
```
