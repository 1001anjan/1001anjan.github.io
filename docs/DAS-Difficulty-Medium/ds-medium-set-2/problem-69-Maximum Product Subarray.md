---
layout: default
title: Maximum Product Subarray
parent: Medium Set 2
grand_parent: DSA Medium
nav_order: 19
permalink: /problem-69-Maximum Product Subarray/
---
# Maximum Product Subarray
Given an integer array nums, find a subarray that has the largest product, and return the product.

The test cases are generated so that the answer will fit in a 32-bit integer.

##### Example 1:
```markdown
Input: nums = [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```
##### Example 2:
```markdown
Input: nums = [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
```
##### Constraints:
* 1 <= nums.length <= 2 * 10^4
* -10 <= nums[i] <= 10
* The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

### Solution:
```java
class Solution {
    public int maxProduct(int[] nums) {
        int max = 1;
        int min = 1;
        int oldMax = 1;
        int ans = Integer.MIN_VALUE;

        for(int i = 0; i < nums.length; i++){
            max = Math.max(max * nums[i], Math.max(nums[i], min * nums[i]));
            min = Math.min(min * nums[i], Math.min(nums[i], oldMax * nums[i]));
            oldMax = max;
            ans = Math.max(ans, max);
        }

        return ans;
    }
}
```