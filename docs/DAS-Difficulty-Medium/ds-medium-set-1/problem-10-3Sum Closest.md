---
layout: default
title: 3Sum Closest
parent: Medium Set 1
grand_parent: DSA Medium Difficulty
nav_order: 10
permalink: /problem-10-3Sum Closest/
---
# 3Sum Closest

Given an integer array nums of length n and an integer target, find three integers in nums such that the sum is closest to target.

Return the sum of the three integers.

You may assume that each input would have exactly one solution.

##### Example 1:
```markdown
Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```
##### Example 2:
```markdown
Input: nums = [0,0,0], target = 1
Output: 0
Explanation: The sum that is closest to the target is 0. (0 + 0 + 0 = 0).
```
##### Constraints:
* 3 <= nums.length <= 500
* -1000 <= nums[i] <= 1000
* -10^4 <= target <= 10^4

### Solution:
```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        int diff = Integer.MAX_VALUE, z = nums.length - 1;
        int ans = 0;
        Arrays.sort(nums);
        for(int i = 0; i < nums.length - 1 && diff != 0; i++){
            int l =  i + 1, u = z;
            while(l < u){
                int s = nums[i] + nums[l] + nums[u];
                int d = target - s;
                if(Math.abs(d) < Math.abs(diff)){
                    diff = d;
                    ans = s;
                }
                if(s < target){
                    l++;
                }else{
                    u--;
                }
            }
        }
        return ans;
    }
}
```