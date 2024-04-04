---
layout: default
title: Keep Multiplying Found Values by Two
parent: Easy Set 11
grand_parent: DSA Easy
nav_order: 25
permalink: /problem-335-Keep Multiplying Found Values by Two/
---
# Keep Multiplying Found Values by Two
You are given an array of integers nums. You are also given an integer original which is the first number that needs to be searched for in nums.

You then do the following steps:

1. If original is found in nums, multiply it by two (i.e., set original = 2 * original).
2. Otherwise, stop the process.
3. Repeat this process with the new number as long as you keep finding the number.
Return the final value of original.

##### Example 1:
```markdown
Input: nums = [5,3,6,1,12], original = 3
Output: 24
Explanation:
- 3 is found in nums. 3 is multiplied by 2 to obtain 6.
- 6 is found in nums. 6 is multiplied by 2 to obtain 12.
- 12 is found in nums. 12 is multiplied by 2 to obtain 24.
- 24 is not found in nums. Thus, 24 is returned.
```
##### Example 2:
```markdown
Input: nums = [2,7,9], original = 4
Output: 4
Explanation:
- 4 is not found in nums. Thus, 4 is returned.
```
##### Constraints:
* 1 <= nums.length <= 1000
* 1 <= nums[i], original <= 1000

### Solution:
```java
class Solution {
    public int findFinalValue(int[] nums, int original) {
        Arrays.sort(nums);
        for(int n : nums){
            if(n == original) original *= 2;
        }
        return original;
    }
}
```
##### Improvement using binary search
```java
class Solution {
    public int findFinalValue(int[] nums, int original) {
        Arrays.sort(nums);
        
        int s = 0;
        int e = nums.length - 1;
        
        while(s <= e){
            int mid = (s + e)/2;
            if(nums[mid] == original){
                original *= 2;
                e = nums.length - 1;
            }else if(nums[mid] > original){
                e = mid - 1;
            }else{
                s = mid + 1;
            }
        }
        
        return original;
    }
}
```
##### But faster approach 
```java
class Solution {
    public int findFinalValue(int[] nums, int original) {
        while(isPresent(nums, original))
            original *= 2;
        return original;
    }
    public boolean isPresent(int[] nums, int target){
        for(int i: nums)
            if(i == target)
                return true;
        
        return false;
    }
}
```