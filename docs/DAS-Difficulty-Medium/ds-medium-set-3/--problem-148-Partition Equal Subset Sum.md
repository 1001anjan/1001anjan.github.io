---
layout: default
title: Partition Equal Subset Sum
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 48
permalink: /problem-148-Partition Equal Subset Sum/
---
# Partition Equal Subset Sum
Given a non-empty array nums containing only positive integers, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

##### Example 1:
```markdown
Input: nums = [1,5,11,5]
Output: true
Explanation: The array can be partitioned as [1, 5, 5] and [11].
```
##### Example 2:
```markdown
Input: nums = [1,2,3,5]
Output: false
Explanation: The array cannot be partitioned into equal sum subsets.
```
##### Constraints:
* 1 <= nums.length <= 200
* 1 <= nums[i] <= 100

### Solution:
##### Time Limit Exceeded
```java
class Solution {
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for(int i = 0; i < nums.length; i++)
            sum += nums[i];

        if(sum % 2 != 0)
            return false;
        
        return dfs(nums, 0, sum / 2);
	
    }

    public boolean dfs(int[] nums, int from, int sum) {
        if(sum == 0)
            return true;
        
        if(sum < 0)
            return false;

        for(int i = from; i < nums.length; i++)
            if(dfs(nums, i + 1, sum - nums[i]))
                return true;
        
        return false;	
    }
}
```
