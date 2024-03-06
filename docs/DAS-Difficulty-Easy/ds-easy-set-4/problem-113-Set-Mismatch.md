---
layout: default
title: Set Mismatch
parent: Easy Set 4
grand_parent: DSA Easy
nav_order: 13
permalink: /problem-113-Set-Mismatch/
---
# Set Mismatch
You have a set of integers s, which originally contains all the numbers from 1 to n. Unfortunately, due to some error, one of the numbers in s got duplicated to another number in the set, which results in repetition of one number and loss of another number.

You are given an integer array nums representing the data status of this set after the error.

Find the number that occurs twice and the number that is missing and return them in the form of an array.

##### Example 1:
```markdown
Input: nums = [1,2,2,4]
Output: [2,3]
```
##### Example 2:
```markdown
Input: nums = [1,1]
Output: [1,2]
```
##### Constraints:
* 2 <= nums.length <= 104
* 1 <= nums[i] <= 104

### Solution:
```java
class Solution {
    public int[] findErrorNums(int[] nums) {
        Set<Integer> set = new HashSet<Integer>();
        Set<Integer> res = new HashSet<Integer>();
        int index = 0;
        // finding duplipactes
        for(int n: nums){
            if(set.contains(n)){
              res.add(n);  
            }else{
                set.add(n);
            }
        }
        // finding missing elements
        for(int i = 1; i<=nums.length; i++){
            if(!set.contains(i)) res.add(i);
        }
        int[] ans = new int[res.size()];
        for(int n: res){
            ans[index++] = n;
        }
        return ans;
    }
}
```
