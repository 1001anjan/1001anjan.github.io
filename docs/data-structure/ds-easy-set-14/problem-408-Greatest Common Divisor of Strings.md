---
layout: default
title: Greatest Common Divisor of Strings
parent: Data Structure Easy Set 14
grand_parent: Data Structure
nav_order: 8
permalink: /problem-408-Greatest Common Divisor of Strings/
---
# Greatest Common Divisor of Strings
For two strings s and t, we say "t divides s" if and only if s = t + ... + t (i.e., t is concatenated with itself one or more times).

Given two strings str1 and str2, return the largest string x such that x divides both str1 and str2.

##### Example 1:
```markdown
Input: str1 = "ABCABC", str2 = "ABC"
Output: "ABC"
```
##### Example 2:
```markdown
Input: str1 = "ABABAB", str2 = "ABAB"
Output: "AB"
```
##### Example 3:
```markdown
Input: str1 = "LEET", str2 = "CODE"
Output: ""
```
##### Constraints:
* 1 <= str1.length, str2.length <= 1000
* str1 and str2 consist of English uppercase letters.

### Solution:
```java
class Solution {
   public String gcdOfStrings(String str1, String str2) {
        if (!(str1+str2).equals(str2+str1))  return "";

        int gcdVal = gcd(str1.length() , str2.length());
        return str2.substring(0, gcdVal);
    }

    public static int gcd(int p, int q) {
        if (q == 0) return p;
        else return gcd(q, p % q);
    }
}
```