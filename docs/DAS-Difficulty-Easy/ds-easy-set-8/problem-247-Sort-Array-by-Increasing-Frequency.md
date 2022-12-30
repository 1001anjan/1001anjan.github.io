---
layout: default
title: Sort Array by Increasing Frequency
parent: Easy Set 8
grand_parent: DSA Easy Difficulty
nav_order: 27
permalink: /problem-247-Sort-Array-by-Increasing-Frequency/
---
# Sort Array by Increasing Frequency
Given an array of integers nums, sort the array in increasing order based on the frequency of the values. If multiple values have the same frequency, sort them in decreasing order.

Return the sorted array.

##### Example 1:
```markdown
Input: nums = [1,1,2,2,2,3]
Output: [3,1,1,2,2,2]
Explanation: '3' has a frequency of 1, '1' has a frequency of 2, and '2' has a frequency of 3.
```
##### Example 2:
```markdown
Input: nums = [2,3,1,3,2]
Output: [1,3,3,2,2]
Explanation: '2' and '3' both have a frequency of 2, so they are sorted in decreasing order.
```
##### Example 3:
```markdown
Input: nums = [-1,1,-6,4,5,-6,1,4,1]
Output: [5,-1,4,4,-6,-6,1,1,1]
```
##### Constraints:
* 1 <= nums.length <= 100
* -100 <= nums[i] <= 100

### Solution:
```java
class Solution {
    public int[] frequencySort(int[] nums) {
        Map<Integer,Integer> map = new HashMap<>();
       
        for(int n : nums){
            map.put(n,map.getOrDefault(n,0) + 1);
        }

        List<Map.Entry<Integer,Integer>> list = new LinkedList<Map.Entry<Integer,Integer>>(map.entrySet());
        
        Collections.sort(list,(i1,i2) -> {
            if(i1.getValue() == i2.getValue()) return i2.getKey().compareTo(i1.getKey());
            else return i1.getValue().compareTo(i2.getValue());
        });
 
        int i = 0;
        for(Map.Entry<Integer,Integer> m : list){
            for(int j = 1; j <= m.getValue(); j++) nums[i++] = m.getKey();
        } 
        
        return nums;
    }
}
```