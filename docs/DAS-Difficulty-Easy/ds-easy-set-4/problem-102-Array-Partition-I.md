---
layout: default
title: Array Partition I
parent: Easy Set 4
grand_parent: DSA Easy Difficulty
nav_order: 2
permalink: /problem-102-Array-Partition-I/
---
#  Array Partition I
Given an integer array nums of 2n integers, group these integers into n pairs (a1, b1), (a2, b2), ..., (an, bn) such that the sum of min(ai, bi) for all i is maximized. Return the maximized sum.

##### Example 1:
```markdown
Input: nums = [1,4,3,2]
Output: 4
Explanation: All possible pairings (ignoring the ordering of elements) are:
1. (1, 4), (2, 3) -> min(1, 4) + min(2, 3) = 1 + 2 = 3
2. (1, 3), (2, 4) -> min(1, 3) + min(2, 4) = 1 + 2 = 3
3. (1, 2), (3, 4) -> min(1, 2) + min(3, 4) = 1 + 3 = 4
   So the maximum possible sum is 4.
```
##### Example 2:
```markdown
Input: nums = [6,2,6,5,1,2]
Output: 9
Explanation: The optimal pairing is (2, 1), (2, 5), (6, 6). min(2, 1) + min(2, 5) + min(6, 6) = 1 + 2 + 6 = 9.
```
##### Constraints:
* 1 <= n <= 104
* nums.length == 2 * n
* -104 <= nums[i] <= 104

### Solution:
```java
class Solution {
    public int arrayPairSum(int[] nums) {
        int max = 0;
        Arrays.sort(nums);
        for(int i = 0; i < nums.length; i = i+2)
            max += nums[i];
        return max;
    }
}
```
#### Counting sort : 
https://leetcode.com/problems/array-partition-i/solution/
```java
class Solution {
    final static int K = 10000;
    
    public int arrayPairSum(int[] nums) {
        // Store the frequency of each element
        int[] elementToCount = new int[2 * K + 1];
        for (int element : nums) {
            // Add K to element to offset negative values
            elementToCount[element + K]++;
        }
        
        // Initialize sum to zero
        int maxSum = 0;
        boolean isEvenIndex = true;
        for (int element = 0; element <= 2 * K; element++) {
            while (elementToCount[element] > 0) {
                // Add element if it is at even position
                maxSum += (isEvenIndex ? element - K : 0);
                // Flip the value (one to zero or zero to one)
                isEvenIndex = !isEvenIndex;
                // Decrement the frequency count
                elementToCount[element]--;
            }
        }
        return maxSum;
    }
}
```