---
layout: default
title: Two Out of Three
parent: Easy Set 11
grand_parent: DSA Easy
nav_order: 4
permalink: /problem-314-Two Out of Three/
---
# Two Out of Three

Given three integer arrays nums1, nums2, and nums3, return a distinct array containing all the values that are present in at least two out of the three arrays. You may return the values in any order.

##### Example 1:
```markdown
Input: nums1 = [1,1,3,2], nums2 = [2,3], nums3 = [3]
Output: [3,2]
Explanation: The values that are present in at least two arrays are:
- 3, in all three arrays.
- 2, in nums1 and nums2.
```
##### Example 2:
```markdown
Input: nums1 = [3,1], nums2 = [2,3], nums3 = [1,2]
Output: [2,3,1]
Explanation: The values that are present in at least two arrays are:
- 2, in nums2 and nums3.
- 3, in nums1 and nums2.
- 1, in nums1 and nums3.
```
##### Example 3:
```markdown
Input: nums1 = [1,2,2], nums2 = [4,3,3], nums3 = [5]
Output: []
Explanation: No value is present in at least two arrays.
```
##### Constraints:
* 1 <= nums1.length, nums2.length, nums3.length <= 100
* 1 <= nums1[i], nums2[j], nums3[k] <= 100

### Solution:
```java
class Solution {
    public List<Integer> twoOutOfThree(int[] nums1, int[] nums2, int[] nums3) {
        Set<Integer> s1 = new HashSet();
        Set<Integer> s2 = new HashSet();
        Set<Integer> s3 = new HashSet();
        
        for(int n : nums1) s1.add(n);
        for(int n : nums2) s2.add(n);
        for(int n : nums3) s3.add(n);
        
        Set<Integer> ans = new HashSet<>();
        
        for(int n : s1){
            if(s2.contains(n) || s2.contains(n)) ans.add(n);
        }
        
        for(int n : s2){
            if(s1.contains(n) || s3.contains(n)) ans.add(n);
        }
        
        for(int n : s3){
            if(s1.contains(n) || s2.contains(n)) ans.add(n);
        }
        
        return new ArrayList(ans);
    }
}
```
##### Improvement
```java
class Solution {
    public List<Integer> twoOutOfThree(int[] nums1, int[] nums2, int[] nums3) {
        //as the max value of a number is limited to 100.. we can use an arrya of size 100.
        
        int[] present = new int[100];
        
        for(int n : nums1) if(present[n - 1] == 0) present[n - 1] += 1;
        for(int n : nums2) if(present[n-1] < 2) present[n - 1] += 2;
        for(int n : nums3) if(present[n - 1] != 0) present[n - 1] += 3;

        List<Integer> result = new ArrayList<>();
        
        for(int i = 0; i < 100; ++i){
            if(present[i] >= 3) result.add(i + 1);
        }
        
        return result;
    }
}
```