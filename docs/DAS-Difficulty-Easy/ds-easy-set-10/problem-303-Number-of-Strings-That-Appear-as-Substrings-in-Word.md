---
layout: default
title: Number of Strings That Appear as Substrings in Word
parent: Easy Set 10
grand_parent: DSA Easy Difficulty
nav_order: 23
permalink: /problem-303-Number of Strings That Appear as Substrings in Word/
---
# Number of Strings That Appear as Substrings in Word

Given an array of strings patterns and a string word, return the number of strings in patterns that exist as a substring in word.

A substring is a contiguous sequence of characters within a string.

##### Example 1:
```markdown
Input: patterns = ["a","abc","bc","d"], word = "abc"
Output: 3
Explanation:
- "a" appears as a substring in "abc".
- "abc" appears as a substring in "abc".
- "bc" appears as a substring in "abc".
- "d" does not appear as a substring in "abc".
  3 of the strings in patterns appear as a substring in word.
```
##### Example 2:
```markdown
Input: patterns = ["a","b","c"], word = "aaaaabbbbb"
Output: 2
Explanation:
- "a" appears as a substring in "aaaaabbbbb".
- "b" appears as a substring in "aaaaabbbbb".
- "c" does not appear as a substring in "aaaaabbbbb".
  2 of the strings in patterns appear as a substring in word.
```

##### Example 3:
```markdown
Input: patterns = ["a","a","a"], word = "ab"
Output: 3
Explanation: Each of the patterns appears as a substring in word "ab".
```
##### Constraints:
* 1 <= patterns.length <= 100
* 1 <= patterns[i].length <= 100
* 1 <= word.length <= 100
* patterns[i] and word consist of lowercase English letters.

### Solution:
```java
class Solution {
    public int numOfStrings(String[] patterns, String word) {
        int c = 0;
        for(String s : patterns){
            if(word.contains(s)) c++;
        }
        return c;
    }
}
```