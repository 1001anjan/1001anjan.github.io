---
layout: default
title: Is Subsequence
parent: Data Structure Easy Set 3
grand_parent: Data Structure
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
        StringBuilder sb = new StringBuilder();
        int j = 0;
        for(int i = 0; i<s.length(); i++){
            while(j<t.length() && s.charAt(i) != t.charAt(j)) j++;
            if(j>=t.length()) break;
            else{
                sb.append(t.charAt(j));
                j++;
            }
        }
        return s.equals(sb.toString());
    }
}
```
