---
layout: default
title: Find Numbers with Even Number of Digits
parent: Easy Set 7
grand_parent: DSA Easy Difficulty
nav_order: 2
permalink: /problem-192-Find-Numbers-with-Even-Number-of-Digits/
---
# Find Numbers with Even Number of Digits

Given an array nums of integers, return how many of them contain an even number of digits.

##### Example 1:
```markdown
Input: nums = [12,345,2,6,7896]
Output: 2
Explanation:
12 contains 2 digits (even number of digits).
345 contains 3 digits (odd number of digits).
2 contains 1 digit (odd number of digits).
6 contains 1 digit (odd number of digits).
7896 contains 4 digits (even number of digits).
Therefore only 12 and 7896 contain an even number of digits.
```

##### Example 2:
```markdown
Input: nums = [555,901,482,1771]
Output: 1
Explanation:
Only 1771 contains an even number of digits.
```
##### Constraints:
* 1 <= nums.length <= 500
* 1 <= nums[i] <= 105

### Solution:
```java
class Solution {
    public int findNumbers(int[] nums) {
        int count = 0;
        for(int n : nums){
            String s = String.valueOf(n);
            if(s.length()%2 == 0) count++;
        }
        return count;
    }
}
```
#### Faster execution
```java
class Solution {
    public int findNumbers(int[] nums) {
       int result=0;
        for(int i=0; i < nums.length;i++){
            if (CalculateDigitsOfNumber(nums[i])%2 == 0){
                result++;
            }
        }
        return result;
    }

    public static int CalculateDigitsOfNumber(int Number){
             return (int)(Math.log10(Number))+1;
    }
}
```