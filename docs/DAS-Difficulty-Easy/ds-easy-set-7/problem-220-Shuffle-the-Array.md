---
layout: default
title: Shuffle the Array
parent: Easy Set 7
grand_parent: DSA Easy
nav_order: 30
permalink: /problem-220-Shuffle-the-Array/
---
# Shuffle the Array
Given the array nums consisting of 2n elements in the form [x1,x2,...,xn,y1,y2,...,yn].

Return the array in the form [x1,y1,x2,y2,...,xn,yn].

##### Example 1:
```markdown
Input: nums = [2,5,1,3,4,7], n = 3
Output: [2,3,5,4,1,7]
Explanation: Since x1=2, x2=5, x3=1, y1=3, y2=4, y3=7 then the answer is [2,3,5,4,1,7].
```
##### Example 2:
```markdown
Input: nums = [1,2,3,4,4,3,2,1], n = 4
Output: [1,4,2,3,3,2,4,1]
```
##### Example 3:
```markdown
Input: nums = [1,1,2,2], n = 2
Output: [1,2,1,2]
```
##### Constraints:
* 1 <= n <= 500
* nums.length == 2n
* 1 <= nums[i] <= 10^3

### Solution:
```java
class Solution {
    public int[] shuffle(int[] nums, int n) {
        int[] ans = new int[nums.length];
        int j = 0;
        int k = n;
        for(int i = 0; i < nums.length; i++){
            if(i%2 == 0){
                ans[i] = nums[j++];
            }else{
                ans[i] = nums[k++];
            }
        }
        return ans;
    }
}
```
#### SAME execution time
```java
class Solution {
    public int[] shuffle(int[] nums, int n) {
        int ans[] = new int[nums.length];
        for(int i = 0; i < nums.length/2; i++){
            ans[i * 2] = nums[i];
            ans[2 * i + 1] = nums[n + i];
        }
        return ans;
    }
}
```