---
layout: default
title: Substrings of Size Three with Distinct Characters
parent: Data Structure Easy Set 10
grand_parent: Data Structure
nav_order: 7
permalink: /problem-287-Substrings-of-Size-Three-with-Distinct-Characters/
---
# Substrings of Size Three with Distinct Characters
A string is good if there are no repeated characters.

Given a string s, return the number of good substrings of length three in s.

Note that if there are multiple occurrences of the same substring, every occurrence should be counted.

A substring is a contiguous sequence of characters in a string.

##### Example 1:
```markdown
Input: s = "xyzzaz"
Output: 1
Explanation: There are 4 substrings of size 3: "xyz", "yzz", "zza", and "zaz".
The only good substring of length 3 is "xyz".
```
##### Example 2:
```markdown
Input: s = "aababcabc"
Output: 4
Explanation: There are 7 substrings of size 3: "aab", "aba", "bab", "abc", "bca", "cab", and "abc".
The good substrings are "abc", "bca", "cab", and "abc".
```
##### Constraints:
* 1 <= s.length <= 100
* s consists of lowercase English letters.

### Solution
```java
class Solution {
    public int countGoodSubstrings(String s) {
        if(s.length() < 3) return 0;
        char prev, now, next;
        prev = s.charAt(0);
        now = s.charAt(1);
        int c = 0;
        for(int i = 1; i < s.length() - 1; i++){
            next = s.charAt(i + 1);
            if(prev != now && prev != next && now != next) c++;
            prev = now;
            now = next;
        }
        return c;
    }
}
```
