---
layout: default
title: Reverse String
parent: Easy Set 2
grand_parent: DSA Easy
nav_order: 30
permalink: /problem-61-b-Reverse-String/
---
# Reverse String

Write a function that reverses a string. The input string is given as an array of characters s.

You must do this by modifying the input array in-place with O(1) extra memory.

##### Example 1:
```markdown
Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```
##### Example 2:
```markdown
Input: s = ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```
##### Constraints:
* 1 <= s.length <= 105
* s[i] is a printable ascii character.

### Solution
```java
class Solution {
    public void reverseString(char[] s) {
        int i = 0;
        int j = s.length - 1;
        char ch;
        while(i<=j){
           ch = s[i];
            s[i] = s[j];
            s[j] = ch;
            i++;
            j--;
        }
    }
}
```