---
layout: default
title: Degree of an Array
parent: Data Structure Easy Set 13
grand_parent: Data Structure
nav_order: 17
permalink: /problem-387-Degree of an Array/
---
# Degree of an Array
Given a non-empty array of non-negative integers nums, the degree of this array is defined as the maximum frequency of any one of its elements.

Your task is to find the smallest possible length of a (contiguous) subarray of nums, that has the same degree as nums.

##### Example 1:
```markdown
Input: nums = [1,2,2,3,1]
Output: 2
Explanation:
The input array has a degree of 2 because both elements 1 and 2 appear twice.
Of the subarrays that have the same degree:
[1, 2, 2, 3, 1], [1, 2, 2, 3], [2, 2, 3, 1], [1, 2, 2], [2, 2, 3], [2, 2]
The shortest length is 2. So return 2.
```
##### Example 2:
```markdown
Input: nums = [1,2,2,3,1,4,2]
Output: 6
Explanation:
The degree is 3 because the element 2 is repeated 3 times.
So [2,2,3,1,4,2] is the shortest subarray, therefore returning 6.
```
##### Constraints:
* nums.length will be between 1 and 50,000.
* nums[i] will be an integer between 0 and 49,999.

### Solution:
```java
class Solution {
    public int findShortestSubArray(int[] nums) {
        Map<Integer, Integer> leftIndex = new HashMap<>(); 
        Map<Integer, Integer> rightIndex = new HashMap<>();
        Map<Integer, Integer> count = new HashMap<>();
        
        for(int i = 0; i < nums.length; i++){
            if(leftIndex.get(nums[i]) == null) leftIndex.put(nums[i],i);
            rightIndex.put(nums[i],i);
            count.put(nums[i],count.getOrDefault(nums[i],0) + 1);
        }
        
        int ans = nums.length;
        int degree = Collections.max(count.values());
        for (int x: count.keySet()) {
            if (count.get(x) == degree) {
                ans = Math.min(ans, rightIndex.get(x) - leftIndex.get(x) + 1);
            }
        }
        return ans;
    }
}
```
```java
class Solution {
    public int findShortestSubArray(int[] nums) {
        if (nums.length == 0 || nums == null) return 0;
        Map<Integer, int[]> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++){
           if (!map.containsKey(nums[i])){
               map.put(nums[i], new int[]{1, i, i});  // the first element in array is degree, second is first index of this key, third is last index of this key
           } else {
               int[] temp = map.get(nums[i]);
               temp[0]++;
               temp[2] = i;
           }
        }
        int degree = Integer.MIN_VALUE, res = Integer.MAX_VALUE;
        for (int[] value : map.values()){
            if (value[0] > degree){
                degree = value[0];
                res = value[2] - value[1] + 1;
            } else if (value[0] == degree){
                res = Math.min( value[2] - value[1] + 1, res);
            } 
        }
        return res;
    }
}
```