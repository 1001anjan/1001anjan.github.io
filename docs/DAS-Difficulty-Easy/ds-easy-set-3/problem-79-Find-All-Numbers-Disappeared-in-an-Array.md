---
layout: default
title: Find All Numbers Disappeared in an Array
parent: Easy Set 3
grand_parent: DSA Easy
nav_order: 16
permalink: /problem-79-Find-All-Numbers-Disappeared-in-an-Array/
---
# Find All Numbers Disappeared in an Array

Given an array nums of n integers where nums[i] is in the range [1, n], return an array of all the integers in the range [1, n] that do not appear in nums.

##### Example 1:
```markdown
Input: nums = [4,3,2,7,8,2,3,1]
Output: [5,6]
```
##### Example 2:
```markdown
Input: nums = [1,1]
Output: [2]
```
##### Constraints:

* n == nums.length
* 1 <= n <= 105
* 1 <= nums[i] <= n

Follow up: Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.

### Solution:
```java
class Solution {
    public List findDisappearedNumbers(int[] arr) {
        int i = 0;
        List<Integer> l = new ArrayList<Integer>();
        while(i<arr.length){
            if(arr[i] == -1){
                i++;
                continue;
            }
            if(arr[arr[i] -1] == -1){
                i++;
                continue;
            }else
            if(arr[i] == i+1){
                arr[i] = -1;
                i++;
            }
            else{
                int t = arr[arr[i]-1];
                arr[arr[i] -1] = -1;
                arr[i] = t;
            }
            
        }
        for(int k = 0; k<arr.length; k++){
            if(arr[k] != -1){
               l.add(k+1); 
            }
        }
        return l;
    }
}
```