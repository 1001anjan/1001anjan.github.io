---
layout: default
title: Counting Words With a Given Prefix
parent: Easy Set 12
grand_parent: DSA Easy
nav_order: 1
permalink: /problem-341-Counting Words With a Given Prefix/
---
# Counting Words With a Given Prefix
You are given an array of strings words and a string pref.

Return the number of strings in words that contain pref as a prefix.

A prefix of a string s is any leading contiguous substring of s.

##### Example 1:
```markdown
Input: words = ["pay","attention","practice","attend"], pref = "at"
Output: 2
Explanation: The 2 strings that contain "at" as a prefix are: "attention" and "attend".
```
##### Example 2:
```markdown
Input: words = ["leetcode","win","loops","success"], pref = "code"
Output: 0
Explanation: There are no strings that contain "code" as a prefix.
```
##### Constraints:
* 1 <= words.length <= 100
* 1 <= words[i].length, pref.length <= 100
* words[i] and pref consist of lowercase English letters.

### Solution:
```java
class Solution {
    public int prefixCount(String[] words, String pref) {
        int c = 0;
        for(String str : words){
            if(str.indexOf(pref) == 0) c++; 
        }
        return c;
    }
}
```