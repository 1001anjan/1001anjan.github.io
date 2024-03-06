---
layout: default
title: Is Subsequence
parent: Easy Set 3
grand_parent: DSA Easy
nav_order: 9
permalink: /problem-72-Is-Subsequence/
---
# Is Subsequence

Given two strings s and t, return true if s is a subsequence of t, or false otherwise.

A subsequence of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., "ace" is a subsequence of "abcde" while "aec" is not).

##### Example 1:
```markdown
Input: s = "abc", t = "ahbgdc"
Output: true
```
##### Example 2:
```markdown
Input: s = "axc", t = "ahbgdc"
Output: false
```
##### Constraints:
* 0 <= s.length <= 100
* 0 <= t.length <= 104
* s and t consist only of lowercase English letters.

### Solution:
```java
class Solution {
    public boolean isSubsequence(String s, String t) {
        int k = 0;
        int l = s.length();
        if(l == 0) return true;
        for(int i = 0; i < t.length(); i++){
            if(t.charAt(i) == s.charAt(k)) k++;
            if(k == l) return true;
        }
        if(k >= l) return true;
        return false;
    }
}
```
```java
class Solution {
    public boolean isSubsequence(String s, String t) {
        
        int i = 0, j = 0;
        int sLength = s.length();
        int tLength = t.length();
        
        while(i < sLength && j < tLength){
            if(s.charAt(i) == t.charAt(j)){
                i++;
            }
            j++;
        }
        
        return i == sLength;
    }
}
```
