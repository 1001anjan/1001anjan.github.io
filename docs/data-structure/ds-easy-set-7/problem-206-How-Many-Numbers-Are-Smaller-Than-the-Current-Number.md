---
layout: default
title: Sort Integers by The Number of 1 Bits
parent: Data Structure Easy Set 7
grand_parent: Data Structure
nav_order: 16
permalink: /problem-206-How Many Numbers Are Smaller Than the Current Number/
---
# How Many Numbers Are Smaller Than the Current Number

Given the array nums, for each nums[i] find out how many numbers in the array are smaller than it. That is, for each nums[i] you have to count the number of valid j's such that j != i and nums[j] < nums[i].

Return the answer in an array.

##### Example 1:
```markdown
Input: nums = [8,1,2,2,3]
Output: [4,0,1,1,3]
Explanation:
For nums[0]=8 there exist four smaller numbers than it (1, 2, 2 and 3).
For nums[1]=1 does not exist any smaller number than it.
For nums[2]=2 there exist one smaller number than it (1).
For nums[3]=2 there exist one smaller number than it (1).
For nums[4]=3 there exist three smaller numbers than it (1, 2 and 2).
```
##### Example 2:
```markdown
Input: nums = [6,5,4,8]
Output: [2,1,0,3]
```
##### Example 3:
```markdown
Input: nums = [7,7,7,7]
Output: [0,0,0,0]
```
##### Constraints:
* 2 <= nums.length <= 500
* 0 <= nums[i] <= 100

### Solution:
```java
class Solution {
    public int[] smallerNumbersThanCurrent(int[] nums) {
        int[] temp = Arrays.copyOf(nums,nums.length);
        Arrays.sort(nums);
        Map<Integer,Integer> m = new HashMap<>();
        m.put(nums[0],0);
        int count = 1;
        for(int i = 1; i < nums.length; i++){
            if(nums[i-1] != nums[i]){
                m.put(nums[i],count);
            }
            count++;
        }
        for(int i = 0; i < temp.length; i++)
            nums[i] = m.get(temp[i]);
        
        return nums;
    }
}
```
```java
class Solution {
    public int[] smallerNumbersThanCurrent(int[] nums) {
        //initiate an array to keep count of all elements in nums
        int[] arr = new int[101];
        for(int num: nums){
            arr[num]++;
        }
        
        //update array by cumulating sum
        for(int i = 1; i < arr.length; i++){
            arr[i] = arr[i] + arr[i-1];
        }
        
        //change the nums array to number of smaller elements than the current number
        //the array arr keep count of elements smaller/equals to each index (element), so to find element smaller than current, look at previous index 
        for(int i = 0; i < nums.length; i++){
            try{
                nums[i] = arr[nums[i]-1];
            } catch (ArrayIndexOutOfBoundsException e){
                nums[i] = 0;
            }
        }
        return nums;
    }
}
```