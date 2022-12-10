---
layout: default
title: Add to Array-Form of Integer
parent: Data Structure Easy Set 5
grand_parent: Data Structure
nav_order: 27
permalink: /problem-157-Add-to-Array-Form-of-Integer/
---
# Add to Array-Form of Integer
The array-form of an integer num is an array representing its digits in left to right order.

* For example, for num = 1321, the array form is [1,3,2,1].
Given num, the array-form of an integer, and an integer k, return the array-form of the integer num + k.

##### Example 1:
```markdown
Input: num = [1,2,0,0], k = 34
Output: [1,2,3,4]
Explanation: 1200 + 34 = 1234
```
##### Example 2:
```markdown
Input: num = [2,7,4], k = 181
Output: [4,5,5]
Explanation: 274 + 181 = 455
```
##### Example 3:
```markdown
Input: num = [2,1,5], k = 806
Output: [1,0,2,1]
Explanation: 215 + 806 = 1021
```
##### Constraints:
* 1 <= num.length <= 104
* 0 <= num[i] <= 9
* num does not contain any leading zeros except for the zero itself.
* 1 <= k <= 104

### Solution:
```java
class Solution {
    public List<Integer> addToArrayForm(int[] nums, int k) {
        LinkedList<Integer> ans = new LinkedList<>();
        int c = 0;
        int i = nums.length - 1;
        while(k>0 || i>=0){
            int d = k%10;
            if(i>=0){
               ans.addFirst((nums[i] + d + c)%10);
                c = (nums[i] + d + c)/10;
                i--;
            }else{
                ans.addFirst((d+c)%10);
                c = (d + c)/10;
            }
            k = k/10;
        }
        if(c>0) ans.addFirst(c);
        return ans;
    }
}
```