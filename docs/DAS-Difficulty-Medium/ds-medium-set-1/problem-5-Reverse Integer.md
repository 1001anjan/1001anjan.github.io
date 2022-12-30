---
layout: default
title: Reverse Integer
parent: Medium Set 1
grand_parent: DSA Medium Difficulty
nav_order: 5
permalink: /problem-5-Reverse Integer/
---
# Reverse Integer
Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-2^31, 2^31 - 1], then return 0.

Assume the environment does not allow you to store 64-bit integers (signed or unsigned).

##### Example 1:
```markdown
Input: x = 123
Output: 321
```
##### Example 2:
```markdown
Input: x = -123
Output: -321
```
##### Example 3:
```markdown
Input: x = 120
Output: 21
```
##### Constraints:
* -2^31 <= x <= 2^31 - 1

### Solution:
```java
class Solution {
    public int reverse(int x) {
        long rev = 0;
        while(x != 0){
            rev = rev * 10 + x %  10;
            x = x / 10;
        }
        if(rev > Integer.MAX_VALUE || rev < Integer.MIN_VALUE) return 0;
        return (int)rev;
    }
}
```
```java
class Solution {
    public int reverse(int x) {
        int rev =0;
        boolean neg = false;
        if(x<0){
            x = x*-1;
            neg = true;
        }
        
        while(x>0){
            if(rev>Integer.MAX_VALUE/10 || (rev == Integer.MAX_VALUE/10 && 
                                         x%10>Integer.MAX_VALUE%10)) 
                return 0;
            rev = rev*10 + x%10 ;
            x = x/10;
        } 
        
        if(neg) return rev*-1;
        return rev;
    }
}
```