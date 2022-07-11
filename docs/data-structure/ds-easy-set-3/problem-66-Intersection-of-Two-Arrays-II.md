---
layout: default
title:  Intersection of Two Arrays II
parent: Data Structure Easy Set 3
grand_parent: Data Structure
nav_order: 3
permalink: /problem-66-Intersection-of-Two-Arrays-II/
---
# Intersection of Two Arrays II

Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must appear as many times as it shows in both arrays and you may return the result in any order.

##### Example 1:
```markdown
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
```
##### Example 2:
```markdown
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
Explanation: [9,4] is also accepted.
```
##### Constraints:
* 1 <= nums1.length, nums2.length <= 1000
* 0 <= nums1[i], nums2[i] <= 1000
 
### Solution
```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int i = 0;
        int j = 0;
        int[] ans = new int[Math.min(nums1.length, nums2.length)];
        int k = 0;
        while(i<nums1.length && j<nums2.length){
            if(nums1[i] == nums2[j]){
                ans[k] = nums1[i];
                k++;
                i++;
                j++;
            }else 
                if(nums1[i]>nums2[j]) j++;
            else
                i++;
        }
        return Arrays.copyOf(ans,k);
    }
}
```