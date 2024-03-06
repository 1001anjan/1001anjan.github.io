---
layout: default
title: Set Mismatch
parent: Easy Set 13
grand_parent: DSA Easy
nav_order: 15
permalink: /problem-385-Set Mismatch/
---
# Set Mismatch
You have a set of integers s, which originally contains all the numbers from 1 to n. Unfortunately, due to some error, one of the numbers in s got duplicated to another number in the set, which results in repetition of one number and loss of another number.

You are given an integer array nums representing the data status of this set after the error.

Find the number that occurs twice and the number that is missing and return them in the form of an array.

##### Example 1:
```markdown
Input: nums = [1,2,2,4]
Output: [2,3]
```
##### Example 2:
```markdown
Input: nums = [1,1]
Output: [1,2]
```
##### Constraints:
* 2 <= nums.length <= 10^4
* 1 <= nums[i] <= 10^4

### Solution: Time Complexity: O(nlogN)
```java
class Solution {
    public int[] findErrorNums(int[] nums) {
        Arrays.sort(nums);
        int dup = 0, miss = 1;
        for(int i = 1; i < nums.length; i++){
            if(nums[i] == nums[i - 1]) dup = nums[i];
            else
            if(nums[i] > nums[i - 1] + 1) miss = nums[i - 1] + 1;
        }
        miss = nums[nums.length - 1] != nums.length? nums.length : miss;
        return new int[]{dup,miss};
    }
}
```

### Solution: Time Complexity O(n) Space Complexity: O(n)
```java
class Solution {
    public int[] findErrorNums(int[] nums) {
        int dup = 0, miss = 0;
        int[] temp = new int[nums.length];
        for(int n : nums) temp[n - 1]++;
        for(int i = 0; i < temp.length; i++){
            if(temp[i] == 0) miss = i + 1;
            else if(temp[i] == 2) dup = i + 1;
        }
       
        return new int[]{dup,miss};
    }
}
```