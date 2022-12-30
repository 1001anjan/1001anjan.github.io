---
layout: default
title: Number of Good Pairs
parent: Easy Set 8
grand_parent: DSA Easy Difficulty
nav_order: 8
permalink: /problem-228-Number-of-Good-Pairs/
---
# Number of Good Pairs

Given an array of integers nums, return the number of good pairs.

A pair (i, j) is called good if nums[i] == nums[j] and i < j.

##### Example 1:
```markdown
Input: nums = [1,2,3,1,1,3]
Output: 4
Explanation: There are 4 good pairs (0,3), (0,4), (3,4), (2,5) 0-indexed.
```
##### Example 2:
```markdown
Input: nums = [1,1,1,1]
Output: 6
Explanation: Each pair in the array are good.
```
##### Example 3:
```markdown
Input: nums = [1,2,3]
Output: 0
```
##### Constraints:
* 1 <= nums.length <= 100
* 1 <= nums[i] <= 100

### Solution:
```java
class Solution {
    public int numIdenticalPairs(int[] nums) {
        int[] count = new int[101];
        for(int n : nums) count[n]++;
        int sum = 0;
        for(int i = 1; i <= 100; i++){
            if(count[i] >= 2){
               sum += (count[i]*(count[i]-1))/2;
            }
        }
        return sum;
    }
}
```