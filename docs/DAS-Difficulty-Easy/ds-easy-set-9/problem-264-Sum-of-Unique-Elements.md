---
layout: default
title: Sum of Unique Elements
parent: Easy Set 9
grand_parent: DSA Easy Difficulty
nav_order: 14
permalink: /problem-264-Sum-of-Unique-Elements/
---
# Sum of Unique Elements
You are given an integer array nums. The unique elements of an array are the elements that appear exactly once in the array.

Return the sum of all the unique elements of nums.

##### Example 1:
```markdown
Input: nums = [1,2,3,2]
Output: 4
Explanation: The unique elements are [1,3], and the sum is 4.
```
##### Example 2:
```markdown
Input: nums = [1,1,1,1,1]
Output: 0
Explanation: There are no unique elements, and the sum is 0.
```
##### Example 3:
```markdown
Input: nums = [1,2,3,4,5]
Output: 15
Explanation: The unique elements are [1,2,3,4,5], and the sum is 15.
```
##### Constraints:
* 1 <= nums.length <= 100
* 1 <= nums[i] <= 100

### Solution:
```java
class Solution {
    public int sumOfUnique(int[] nums) {
        int[] dp = new int[101];
        for(int n : nums) dp[n]++;
        int sum = 0;
        int i = 0;
        for(int n : dp){
            if(n == 1) sum += i;
            i++;
        }
        
        return sum;
    }
}
```
