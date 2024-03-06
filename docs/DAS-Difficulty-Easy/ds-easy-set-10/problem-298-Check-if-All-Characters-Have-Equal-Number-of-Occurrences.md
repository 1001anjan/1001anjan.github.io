---
layout: default
title: Check if All Characters Have Equal Number of Occurrences
parent: Easy Set 10
grand_parent: DSA Easy
nav_order: 18
permalink: /problem-298-Check if All Characters Have Equal Number of Occurrences/
---
# Check if All Characters Have Equal Number of Occurrences
Given a string s, return true if s is a good string, or false otherwise.

A string s is good if all the characters that appear in s have the same number of occurrences (i.e., the same frequency).

##### Example 1:
```markdown
Input: s = "abacbc"
Output: true
Explanation: The characters that appear in s are 'a', 'b', and 'c'. All characters occur 2 times in s.
```
##### Example 2:
```markdown
Input: s = "aaabb"
Output: false
Explanation: The characters that appear in s are 'a' and 'b'.
'a' occurs 3 times while 'b' occurs 2 times, which is not the same number of times.
```
##### Constraints:
* 1 <= s.length <= 1000
* s consists of lowercase English letters.

### Solution:
```java
class Solution {
    public boolean areOccurrencesEqual(String s) {
        int[] dp = new int[26];
        for(char c : s.toCharArray()) dp[c - 'a']++;
        int i = 0;
        while(i < 26 && dp[i] == 0) i++;
        // since we have atleast one char
        int p = dp[i];
        while(i < 26){
            if(dp[i] != 0 && dp[i] != p) return false;
            i++;
        }
        return true;
    }
}
```