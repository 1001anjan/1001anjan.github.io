---
layout: default
title: Base 7
parent: Easy Set 3
grand_parent: DSA Easy Difficulty
nav_order: 28
permalink: /problem-91-Base-7/
---
# Base 7

Given an integer num, return a string of its base 7 representation.

##### Example 1:
```markdown
Input: num = 100
Output: "202"
```
##### Example 2:
```markdown
Input: num = -7
Output: "-10"
```
##### Constraints:
* -107 <= num <= 107

### Solution:
```java
class Solution {
    public String convertToBase7(int num) {
        if(num == 0) return "0";
        boolean sign = false;
        if(num<0){
            num = num*-1;
            sign = true;
        }
        StringBuffer sb = new StringBuffer();
        int base7 = 0;
        while(num>0){
           sb.append(num%7) ;
            num = num/7;
        }
        if(sign)
            return "-" + sb.reverse().toString();
        else
            return  sb.reverse().toString();
    }
}
```