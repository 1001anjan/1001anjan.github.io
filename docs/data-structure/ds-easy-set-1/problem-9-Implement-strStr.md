---
layout: default
title: Implement strStr()
parent: Data Structure Easy Set 1
grand_parent: Data Structure
nav_order: 9
permalink: /problem-9-implement-strStr/
---
# Implement strStr()

Implement strStr().

Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

### Clarification:

What should we return when needle is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when needle is an empty string. This is consistent to C's strstr() and Java's indexOf().



#### Example 1:
```markdown
Input: haystack = "hello", needle = "ll"
Output: 2
```
#### Example 2:
```markdown
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

### Constraints:

* 1 <= haystack.length, needle.length <= 104
* haystack and needle consist of only lowercase English characters.

### Solution
```java
class Solution {
    public int strStr(String haystack, String needle) {
        if(needle.equals("") || needle == null) return 0;
        int j = 0;
        int res = -1;
        for(int i=0; i<haystack.length(); i++){
            if(haystack.charAt(i) == needle.charAt(j)){
                if(j == 0){
                   res = i; 
                } 
                j++;
                if(j == needle.length()) return res;
            }else{
                if(res != -1){
                    i = res;
                }
                res = -1;
                j = 0;
            }
        }
        if(j != needle.length()) return -1;
        return res;
    }
}
```