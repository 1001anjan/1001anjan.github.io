---
layout: default
title: Make Array Zero by Subtracting Equal Amounts
parent: Easy Set 12
grand_parent: DSA Easy
nav_order: 28
permalink: /problem-368-Make Array Zero by Subtracting Equal Amounts/
---
# Make Array Zero by Subtracting Equal Amounts
You are given a non-negative integer array nums. In one operation, you must:

* Choose a positive integer x such that x is less than or equal to the smallest non-zero element in nums.
* Subtract x from every positive element in nums.
Return the minimum number of operations to make every element in nums equal to 0.

##### Example 1:
```markdown
Input: nums = [1,5,0,3,5]
Output: 3
Explanation:
In the first operation, choose x = 1. Now, nums = [0,4,0,2,4].
In the second operation, choose x = 2. Now, nums = [0,2,0,0,2].
In the third operation, choose x = 2. Now, nums = [0,0,0,0,0].
```
##### Example 2:
```markdown
Input: nums = [0]
Output: 0
Explanation: Each element in nums is already 0 so no operations are needed.
```
##### Constraints:
* 1 <= nums.length <= 100
* 0 <= nums[i] <= 100

### Solution:
```java
class Solution {
    public int minimumOperations(int[] nums) {
        int c = 0;
        Arrays.sort(nums);
        int prev = 0;
        for(int n : nums){
            if(n - prev != 0) c++;
            prev = n;
        }
        return c;
    }
}
```
##### O(n) complexity
```java
class Solution {
    public int minimumOperations(int[] nums) {
        int c = 0;
        boolean[] dp = new boolean[101];
        for(int n : nums){
            if(n == 0) continue;
            if(!dp[n]){
                dp[n] = true;
                c++;
            }
        }
        return c;
    }
}
```