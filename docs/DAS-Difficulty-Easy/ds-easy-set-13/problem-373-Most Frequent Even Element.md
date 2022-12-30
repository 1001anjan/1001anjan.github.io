---
layout: default
title: Most Frequent Even Element
parent: Easy Set 13
grand_parent: DSA Easy Difficulty
nav_order: 3
permalink: /problem-373-Most Frequent Even Element/
---
# Most Frequent Even Element
Given an integer array nums, return the most frequent even element.

If there is a tie, return the smallest one. If there is no such element, return -1.

##### Example 1:
```markdown
Input: nums = [0,1,2,2,4,4,1]
Output: 2
Explanation:
The even elements are 0, 2, and 4. Of these, 2 and 4 appear the most.
We return the smallest one, which is 2.
```
##### Example 2:
```markdown
Input: nums = [4,4,4,9,2,4]
Output: 4
Explanation: 4 is the even element appears the most.
```
##### Example 3:
```markdown
Input: nums = [29,47,21,41,13,37,25,7]
Output: -1
Explanation: There is no even element.
```
##### Constraints:
* 1 <= nums.length <= 2000
* 0 <= nums[i] <= 10^5

### Solution:
```java
class Solution {
    public int mostFrequentEven(int[] nums) {
        int max = 0;
        Arrays.sort(nums);
        int prev = -1;
        int count = 0;
        int element = -1;
        for(int n : nums){
            if(n != prev) count = 0;
            if(n % 2 == 0) count++;
            if(count > max){
                element = n;
                max = count;
            }
            prev = n;
        }
        return element;
    }
}
```