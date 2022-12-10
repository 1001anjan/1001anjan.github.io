---
layout: default
title: 3Sum
parent: Data Structure Medium Set 1
grand_parent: Data Structure
nav_order: 9
permalink: /problem-9-3Sum/
---
# 3Sum
Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

##### Example 1:
```markdown
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation:
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.
```
##### Example 2:
```markdown
Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.
```
##### Example 3:
```markdown
Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.
```
##### Constraints:
* 3 <= nums.length <= 3000
* -10^5 <= nums[i] <= 10^5

### Solution:
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Set<List<Integer>> ans = new HashSet<>();
        Arrays.sort(nums);
        System.out.println();
        
        for(int i = 0; i < nums.length - 1; i++){
            int l = i + 1;
            int u = nums.length - 1;
            while(l < u){
                int s = nums[l] + nums[u] + nums[i];
                if(s == 0){
                    ans.add(Arrays.asList(nums[i], nums[l], nums[u]));
                    l++;
                    u--;
                }else if(s > 0){
                    u--;
                }else{
                    l++;
                }
            }
        }
        return new ArrayList(ans);
    }
}
```