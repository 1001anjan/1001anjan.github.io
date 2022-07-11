---
layout: default
title: Add Strings
parent: Data Structure Easy Set 3
grand_parent: Data Structure
nav_order: 14
permalink: /problem-77-Add-Strings/
---
# Add Strings

Given two non-negative integers, num1 and num2 represented as string, return the sum of num1 and num2 as a string.

You must solve the problem without using any built-in library for handling large integers (such as BigInteger). You must also not convert the inputs to integers directly.

##### Example 1:
```markdown
Input: num1 = "11", num2 = "123"
Output: "134"
```
##### Example 2:
```markdown
Input: num1 = "456", num2 = "77"
Output: "533"
```
##### Example 3:
```markdown
Input: num1 = "0", num2 = "0"
Output: "0"
```
##### Constraints:

* 1 <= num1.length, num2.length <= 104
* num1 and num2 consist of only digits.
* num1 and num2 don't have any leading zeros except for the zero itself.

##### Solution:
```java
class Solution {
    public String addStrings(String num1, String num2) {
        int c = 0;
        int v;
        int i = num1.length() - 1;
        int j = num2.length() - 1;
        StringBuilder sb = new StringBuilder();
        while(i>=0 && j>=0){
            v = (num1.charAt(i) -48 + num2.charAt(j) -48 + c)%10;
            c = (num1.charAt(i) -48 + num2.charAt(j) -48 + c)/10;
            sb.append(v);
            i--;
            j--;

        }
        while(i>=0){
            v = (num1.charAt(i) -48 + c)%10;
            c = (num1.charAt(i) -48 + c)/10;
            sb.append(v);
            i--;
        }
        while(j>=0){
            v = (num2.charAt(j) -48 + c)%10;
            c = (num2.charAt(j) -48 + c)/10;
            sb.append(v);
            j--;
        }
        if(c>=1) sb.append(c);
        return sb.reverse().toString();
    }
}
```