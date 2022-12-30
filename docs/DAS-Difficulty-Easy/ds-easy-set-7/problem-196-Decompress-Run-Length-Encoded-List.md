---
layout: default
title: Decompress Run-Length Encoded List
parent: Easy Set 7
grand_parent: DSA Easy Difficulty
nav_order: 6
permalink: /problem-196-Decompress-Run-Length-Encoded-List/
---
# Decompress Run-Length Encoded List

We are given a list nums of integers representing a list compressed with run-length encoding.

Consider each adjacent pair of elements [freq, val] = [nums[2*i], nums[2*i+1]] (with i >= 0).  For each such pair, there are freq elements with value val concatenated in a sublist. Concatenate all the sublists from left to right to generate the decompressed list.

Return the decompressed list.

##### Example 1:
```markdown
Input: nums = [1,2,3,4]
Output: [2,4,4,4]
Explanation: The first pair [1,2] means we have freq = 1 and val = 2 so we generate the array [2].
The second pair [3,4] means we have freq = 3 and val = 4 so we generate [4,4,4].
At the end the concatenation [2] + [4,4,4] is [2,4,4,4].
```
##### Example 2:
```markdown
Input: nums = [1,1,2,3]
Output: [1,3,3]
```
##### Constraints:
* 2 <= nums.length <= 100
* nums.length % 2 == 0
* 1 <= nums[i] <= 100

### Solution:
```java
class Solution {
    public int[] decompressRLElist(int[] nums) {
        List<Integer> ans = new ArrayList<>();
        for(int i = 0; i <= nums.length-2; i = i+2){
            while(nums[i] > 0){
                ans.add(nums[i+1]);
                nums[i]--;
            }
        }
        int[] res = new int[ans.size()];
        int i = 0;
        for(int n : ans) res[i++] = n;
        return res;
    }
}
```
#### Faster approach 
```java
class Solution {
    public int[] decompressRLElist(int[] nums) {
        int size=0;
        
        for(int i=0;i<nums.length;i+=2) size+=nums[i];
        
        int arr[] = new int[size];
        int j=0;
        
        for(int i=0; i<nums.length; i+=2){
            while(nums[i]>0){
                arr[j] = nums[i+1];
                j++;
                nums[i]--;
            }
        }
        return arr;
    }
}
```