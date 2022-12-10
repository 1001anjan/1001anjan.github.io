---
layout: default
title: Second Largest Digit in a String
parent: Data Structure Easy Set 9
grand_parent: Data Structure
nav_order: 23
permalink: /problem-273-Second-Largest-Digit-in-a-String/
---
# Second Largest Digit in a String
Given an alphanumeric string s, return the second largest numerical digit that appears in s, or -1 if it does not exist.

An alphanumeric string is a string consisting of lowercase English letters and digits.

##### Example 1:
```markdown
Input: s = "dfa12321afd"
Output: 2
Explanation: The digits that appear in s are [1, 2, 3]. The second largest digit is 2.
```
##### Example 2:
```markdown
Input: s = "abc1111"
Output: -1
Explanation: The digits that appear in s are [1]. There is no second largest digit.
```
##### Constraints:
* 1 <= s.length <= 500
* s consists of only lowercase English letters and/or digits.

### Solution:
```java
class Solution {
    public int secondHighest(String s) {
        boolean[] d = new boolean[10];
        for(char c : s.toCharArray()){
            if(!Character.isLetter(c)){
                d[c - '0'] = true;
            }
        }
        int i = 9;
        while(i >= 0 && !d[i]) i--;
        if(i == 0 || i == -1) return -1;
        i--;
        while(i >= 0 && !d[i]) i--;
        return i;
    }
}
```
#### naturally faster approach
```java
class Solution {
    public int secondHighest(String s) {
        int first = -1;
        int second = -1;
        for(char c : s.toCharArray()) {
            if(c >= '0' && c <= '9') {
                int num = c - '0';
                if(num > first) {
                    second = first;
                    first = num;
                } else if(num > second && num < first) {
                    second = num;
                }
            }
        }
        return second;
    }
}
```