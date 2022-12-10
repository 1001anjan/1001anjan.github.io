---
layout: default
title: Check If All 1's Are at Least Length K Places Away
parent: Data Structure Easy Set 7
grand_parent: Data Structure
nav_order: 24
permalink: /problem-214-Check-If-All-1's-Are-at-Least-Length-K-Places-Away/
---
# Check If All 1's Are at Least Length K Places Away

Given an binary array nums and an integer k, return true if all 1's are at least k places away from each other, otherwise return false.

#####Example 1:
![](../../assets/images/ds/sample_1_1791.png)

```markdown
Input: nums = [1,0,0,0,1,0,0,1], k = 2
Output: true
Explanation: Each of the 1s are at least 2 places away from each other.
```
##### Example 2:

```markdown
Input: nums = [1,0,0,1,0,1], k = 2
Output: false
Explanation: The second 1 and third 1 are only one apart from each other.
```
##### Constraints:
* 1 <= nums.length <= 105
* 0 <= k <= nums.length
* nums[i] is 0 or 1

### Solution:
```java
class Solution {
    public boolean kLengthApart(int[] nums, int k) {
        // initialize the counter of zeros to k
        // to pass the first 1 in nums
        int count = k;
        
        for (int num : nums) {
            // if the current integer is 1
            if (num == 1) {
                // check that number of zeros in-between 1s
                // is greater than or equal to k
                if (count < k) {
                    return false;    
                }
                // reinitialize counter
                count = 0;
                
            // if the current integer is 0
            } else {
                // increase the counter
                ++count;    
            } 
        }        
        return true;
    }
}
```

##### Bit manipulation 
https://leetcode.com/problems/check-if-all-1s-are-at-least-length-k-places-away/solution/
```java
class Solution {
    public boolean kLengthApart(int[] nums, int k) {
        // convert binary array into int
        int x = 0;
        for (int num : nums) {
            x = (x << 1) | num;    
        }
        
        // base case
        if (x == 0 || k == 0) {
            return true;    
        }
        
        // remove trailing zeros
        while ((x & 1) == 0) {
            x = x >> 1;    
        }
        
        while (x != 1) {
            // remove trailing 1-bit
            x = x >> 1;
            
            // count trailing zeros
            int count = 0;
            while ((x & 1) == 0) {
                x = x >> 1;
                ++count;    
            }
                
            // number of zeros in-between 1-bits
            // should be greater than or equal to k
            if (count < k) {
                return false;    
            }    
        }
        return true;
    }
}
```