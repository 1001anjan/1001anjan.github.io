---
layout: default
title: Find the Index of the First Occurrence in a String
parent: Medium Set 1
grand_parent: DSA Medium
nav_order: 15
permalink: /problem-15-Find the Index of the First Occurrence in a String/
---
# Find the Index of the First Occurrence in a String
Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

##### Example 1:
```markdown
Input: haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.
```
##### Example 2:
```markdown
Input: haystack = "leetcode", needle = "leeto"
Output: -1
Explanation: "leeto" did not occur in "leetcode", so we return -1.
```
##### Constraints:
* 1 <= haystack.length, needle.length <= 104
* haystack and needle consist of only lowercase English characters.

### Solution: 
```java
class Solution {
    public int strStr(String haystack, String needle) {
        return haystack.indexOf(needle);
    }
}
```
```java
class Solution {
    public int strStr(String haystack, String needle) {
        int i = 0, j = 0;
        int n1 = haystack.length();
        int n2 = needle.length();

        while(i <= n1 - n2){
            if(i <= n1 - n2 && haystack.charAt(i) != needle.charAt(0)) i++;
            int k = i;
            while(k < n1 && j < n2 && haystack.charAt(k) == needle.charAt(j)){
                k ++;
                j ++;
            } 
            if(j == n2) return i;
            j = 0;
            i++;
        }

        return -1;
    }
}
```