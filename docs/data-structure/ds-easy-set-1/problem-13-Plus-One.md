---
layout: default
title: Plus One
parent: Data Structure Easy Set 1
grand_parent: Data Structure
nav_order: 13
permalink: /problem-13-plus-one/
---
# Plus One

You are given a large integer represented as an integer array digits, where each digits[i] is the ith digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.

Increment the large integer by one and return the resulting array of digits.

#### Example 1:
```markdown
Input: digits = [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Incrementing by one gives 123 + 1 = 124.
Thus, the result should be [1,2,4].
```
#### Example 2:
```markdown
Input: digits = [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
Incrementing by one gives 4321 + 1 = 4322.
Thus, the result should be [4,3,2,2].
```
#### Example 3:
```markdown
Input: digits = [9]
Output: [1,0]
Explanation: The array represents the integer 9.
Incrementing by one gives 9 + 1 = 10.
Thus, the result should be [1,0].
```

### Constraints:

* 1 <= digits.length <= 100
* 0 <= digits[i] <= 9
* digits does not contain any leading 0's.

### Solution
```java
class Solution {
    public int[] plusOne(int[] digits) {
        
        for(int i=digits.length-1; i>=0; i--){
            if(digits[i] < 9){
                digits[i] = digits[i] + 1;
                break;
            }else{
                digits[i] = 0;
            }
        }
        
        if(digits[0] == 0){
            int[] updatedDigits = new int[digits.length+1];
            updatedDigits[0] = 1;
            
            for(int i=0; i<digits.length; i++){
                updatedDigits[i+1] = digits[i];
            }
            
            return updatedDigits;
        }
        
        return digits;
    }
}
```
### Other
```java
class Solution {
    public int[] plusOne(int[] digits) {
        int []result = new int[digits.length+1];
        result[digits.length] = (digits[digits.length-1]+1)%10;
        int c = (digits[digits.length-1]+1)/10;
        digits[digits.length-1] = (digits[digits.length-1]+1)%10;
        int c1 = c;
        for(int i = digits.length-2; i>=0; i--){
            result[i+1] = (digits[i]+c1)%10;
            c = (digits[i]+c)/10;
            digits[i] = (digits[i]+c1)%10;
            c1 = c;
        }
        result[0] = c;
        if(c>0){
            return result;
        }
        return digits;
    }
}
```