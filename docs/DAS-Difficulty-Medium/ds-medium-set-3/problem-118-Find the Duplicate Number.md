---
layout: default
title: Find the Duplicate Number
parent: Medium Set 3
grand_parent: DSA Medium
nav_order: 18
permalink: /problem-118-Find the Duplicate Number/
---
# Find the Duplicate Number
Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive.

There is only one repeated number in nums, return this repeated number.

You must solve the problem without modifying the array nums and uses only constant extra space.

##### Example 1:
```markdown
Input: nums = [1,3,4,2,2]
Output: 2
```
##### Example 2:
```markdown
Input: nums = [3,1,3,4,2]
Output: 3
```
##### Constraints:
* 1 <= n <= 10^5
* nums.length == n + 1
* 1 <= nums[i] <= n
* All the integers in nums appear only once except for precisely one integer which appears two or more times.

##### Follow up:
* How can we prove that at least one duplicate number must exist in nums?
* Can you solve the problem in linear runtime complexity?

### Solution:
### Using cycle detection
```java
class Solution {
    public int findDuplicate(int[] nums) {
       int slow = 0;
       int fast = 0;

       do{
           slow = nums[slow];
           fast = nums[nums[fast]];
       }while(slow != fast); 

       fast = 0;
       do{
           slow = nums[slow];
           fast = nums[fast];
       }while(slow != fast);

       return slow;
    }
}
```

### Using swap
```java
class Solution {
    public int findDuplicate(int[] nums) {
        while(nums[0] != nums[nums[0]]){
            int n = nums[nums[0]];
            nums[nums[0]] = nums[0];
            nums[0] = n;
        }

        return nums[0];
    }
}
```