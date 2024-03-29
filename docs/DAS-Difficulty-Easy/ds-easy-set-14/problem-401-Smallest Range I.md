---
layout: default
title: Smallest Range I
parent: Easy Set 14
grand_parent: DSA Easy
nav_order: 1
permalink: /problem-401-Smallest Range I/
---
##### Smallest Range I
You are given an integer array nums and an integer k.

In one operation, you can choose any index i where 0 <= i < nums.length and change nums[i] to nums[i] + x where x is an integer from the range [-k, k]. You can apply this operation at most once for each index i.

The score of nums is the difference between the maximum and minimum elements in nums.

Return the minimum score of nums after applying the mentioned operation at most once for each index in it.

##### Example 1:
```markdown
Input: nums = [1], k = 0
Output: 0
Explanation: The score is max(nums) - min(nums) = 1 - 1 = 0.
```
##### Example 2:
```markdown
Input: nums = [0,10], k = 2
Output: 6
Explanation: Change nums to be [2, 8]. The score is max(nums) - min(nums) = 8 - 2 = 6.
```
##### Example 3:
```markdown
Input: nums = [1,3,6], k = 3
Output: 0
Explanation: Change nums to be [4, 4, 4]. The score is max(nums) - min(nums) = 4 - 4 = 0.
```
##### Constraints:
* 1 <= nums.length <= 10^4
* 0 <= nums[i] <= 10^4
* 0 <= k <= 10^4

### Solution:
```java
class Solution {
    public int smallestRangeI(int[] nums, int k) {
        int max = -1, min = Integer.MAX_VALUE;
        for(int n : nums){
            max = Math.max(max,n);
            min = Math.min(min,n);
        }
        if((max - min) <= 2*k) return 0;
        return max - k - min - k;
    }
}
```