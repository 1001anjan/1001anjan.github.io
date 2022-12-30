---
layout: default
title: N-Repeated Element in Size 2N Array
parent: Easy Set 5
grand_parent: DSA Easy Difficulty
nav_order: 23
permalink: /problem-153-N-Repeated-Element-in-Size-2N-Array/
---
# N-Repeated Element in Size 2N Array
You are given an integer array nums with the following properties:

* nums.length == 2 * n.
* nums contains n + 1 unique elements.
* Exactly one element of nums is repeated n times.

Return the element that is repeated n times.

##### Example 1:
```markdown
Input: nums = [1,2,3,3]
Output: 3
```
##### Example 2:
```markdown
Input: nums = [2,1,2,5,3,2]
Output: 2
```
##### Example 3:
```markdown
Input: nums = [5,1,5,2,5,3,5,4]
Output: 5
```
##### Constraints:
* 2 <= n <= 5000
* nums.length == 2 * n
* 0 <= nums[i] <= 104
* nums contains n + 1 unique elements and one of them is repeated exactly n times.

### Solution:
```java
class Solution {
    public int repeatedNTimes(int[] nums) {
        Map<Integer,Integer> map = new HashMap<>();
        
        for(int n:nums)
            map.put(n,map.getOrDefault(n,0) + 1);
        
        for(int n: map.keySet())
            // since others elemements are unique 
            if(map.get(n)>1) return n;
        throw null;
    }
}
```
If we ever find a repeated element, it must be the answer. Let's call this answer the major element.

Consider all subarrays of length 4. There must be a major element in at least one such subarray.

This is because either:

* There is a major element in a length 2 subarray, or;
* Every length 2 subarray has exactly 1 major element, which means that a length 4 subarray that begins at a major element will have 2 major elements.
Thus, we only have to compare elements with their neighbors that are distance 1, 2, or 3 away.
```java
class Solution {
    public int repeatedNTimes(int[] nums) {
        for(int k = 1; k<=3; k++){
            for(int i=0; i<nums.length-k; i++)
                if(nums[i] == nums[i+k]) return nums[i];
        }
        throw null;
    }
}
```