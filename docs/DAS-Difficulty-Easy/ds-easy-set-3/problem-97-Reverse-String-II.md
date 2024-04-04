---
layout: default
title: Reverse String II
parent: Easy Set 3
grand_parent: DSA Easy
nav_order: 34
permalink: /problem-97-Reverse-String-II/
---
# Reverse String II

Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.

f there are fewer than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and leave the other as original.

##### Example 1:
```markdown
Input: s = "abcdefg", k = 2
Output: "bacdfeg"
```
##### Example 2:
```markdown
Input: s = "abcd", k = 2
Output: "bacd"
```
##### Constraints:
* 1 <= s.length <= 104
* s consists of only lowercase English letters.
* 1 <= k <= 104

### Solution:
```java
class Solution {
    public String reverseStr(String s, int k) {
        int p = 0;
        char [] str = s.toCharArray();
        while(p<str.length){
            // if reverse segment 
            int l = p;
            int u = p + k -1;
            
            if(u >= str.length)
                u = str.length - 1;
             
            while(l<u){
                char ch = str[l];
                str[l] = str[u];
                str[u] = ch;
                l++;
                u--;
            }
            p = p + 2*k;
        }
        return new String(str);
    }
}
```