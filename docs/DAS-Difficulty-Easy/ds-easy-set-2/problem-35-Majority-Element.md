---
layout: default
title: Majority Element
parent: Easy Set 2
grand_parent: DSA Easy
nav_order: 4
permalink: /problem-35-Majority-Element/
---
# Majority Element
Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

##### Example 1:
```markdown
Input: nums = [3,2,3]
Output: 3
```
##### Example 2:
```markdown
Input: nums = [2,2,1,1,1,2,2]
Output: 2
```
##### Constraints:
* n == nums.length
* 1 <= n <= 5 * 104
* -109 <= nums[i] <= 109

### Solution
##### Sorting Approach: NlogN complexity. Space: O(1)
```java
class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length/2];
    }
}
```
##### HashMap Approach: Time Complexity O(n), Space Complexity: O(n)
```java
class Solution {
    public int majorityElement(int[] nums) {
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        for(int i=0; i<nums.length; i++){
            if(map.containsKey(nums[i])){
                map.put(nums[i],map.get(nums[i])+1);
            }else{
                map.put(nums[i],1);
            }
        }
        int count = 0;
        int key = 0;
        for(Map.Entry<Integer,Integer> keyValue : map.entrySet()){
            if(keyValue.getValue()>count){
                count = keyValue.getValue();
                key = keyValue.getKey();
            } 
        }
        return key;
    }
}
```
##### Moor's Algorithm: Time Complexity: O(n), Space Complexity: O(1) 
```java
class Solution {
    public int majorityElement(int[] nums) {
        if(nums.length == 1) return nums[0];
        int majorElementIndex = 0;
        int majorElementCount = 1;
        for(int i=1; i<nums.length; i++){
            if(nums[majorElementIndex] == nums[i]){
                majorElementCount ++;
            }else{
                majorElementCount --;
            }
            if(majorElementCount == 0){
                majorElementCount = 1;
                majorElementIndex = i;
            }
        }
        return nums[majorElementIndex];
    }
}
```