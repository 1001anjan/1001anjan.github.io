---
layout: default
title: Jump Game
parent: Medium Set 1
grand_parent: DSA Medium Difficulty
nav_order: 30
permalink: /problem-30-Jump Game/
---
# Jump Game
You are given an integer array nums. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position.

Return true if you can reach the last index, or false otherwise.

##### Example 1:
```markdown
Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```
##### Example 2:
```markdown
Input: nums = [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.
```
##### Constraints:
* 1 <= nums.length <= 10^4
* 0 <= nums[i] <= 10^5

### Solution:
```java
class Solution {
    public boolean canJump(int[] nums) {
        boolean[] dp = new boolean[nums.length];
        return testJump(nums,0, dp);
    }

    public boolean testJump(int[] arr, int start, boolean[] dp){
        if(start >= arr.length - 1) return true;
        if(arr[start] == 0) return false;

        boolean status = false;
        for(int i = start + 1; i <= start + arr[start]; i++){
            if(i >= arr.length - 1) return true;
            if(!dp[i]){
                dp[i] = true;
                status = status | testJump(arr, i, dp);
            }
        }
        return status;
    }
}
```
```java
class Solution {
    //we can use dynamic programming.
    //for a given position i
    //OPT[i] represent whether it is possible to reach the last index or not.
    //OPT[i] = true if (i == last Index)
    //OPT[i] = OPT[i+1] || OPT[i+2] || ... }} OPT[i+nums[i]]
    //OPT[i] = false if (nums[i] == 0)
    //The result is opt[0];
    public boolean canJump(int[] nums) {
        boolean[] dp = new boolean[nums.length];
        Arrays.fill(dp, false);
        dp[nums.length-1] = true;
        for(int i = nums.length - 2; i >= 0; i--){
            if(nums[i] == 0)
                dp[i] = false;
            else{
                if(nums[i] + i >= nums.length)
                    dp[i] = true;
                else{
                   for(int j = 1; j <= nums[i]; j++){
                       dp[i] = dp[i] || dp[i + j];
                       //tricky part: the next recurrance is aslo cover some elements for this value so that we can skip them.
                       j += nums[i + j];
                   } 
                }
            }
        }
        
        return dp[0];
    }
}
```
Assume that we can move step = nums[0] steps at the beginning, then move to num[1] and step--, always take the max of num[1] and step as remaining steps, and repeat until arriving at the last element. If step == 0 during the iteration, it means we could neither move forward nor reach the end, so return false.

```java
class Solution {
    public boolean canJump(int[] nums) {
        int step = nums[0];
        for (int i = 1; i < nums.length; i++) {
            if (step == 0) return false;
            step = Math.max(--step, nums[i]);
        }
        return true;
    }
}
```