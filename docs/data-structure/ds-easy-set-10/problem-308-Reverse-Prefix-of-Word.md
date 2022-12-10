---
layout: default
title: Reverse Prefix of Word
parent: Data Structure Easy Set 10
grand_parent: Data Structure
nav_order: 28
permalink: /problem-308-Reverse-Prefix-of-Word/
---
# Reverse Prefix of Word

Given a 0-indexed string word and a character ch, reverse the segment of word that starts at index 0 and ends at the index of the first occurrence of ch (inclusive). If the character ch does not exist in word, do nothing.

For example, if word = "abcdefd" and ch = "d", then you should reverse the segment that starts at 0 and ends at 3 (inclusive). The resulting string will be "dcbaefd".
Return the resulting string.

##### Example 1:
```markdown
Input: word = "abcdefd", ch = "d"
Output: "dcbaefd"
Explanation: The first occurrence of "d" is at index 3.
Reverse the part of word from 0 to 3 (inclusive), the resulting string is "dcbaefd".
```
##### Example 2:
```markdown
Input: word = "xyxzxe", ch = "z"
Output: "zxyxxe"
Explanation: The first and only occurrence of "z" is at index 3.
Reverse the part of word from 0 to 3 (inclusive), the resulting string is "zxyxxe".
```
##### Example 3:
```markdown
Input: word = "abcd", ch = "z"
Output: "abcd"
Explanation: "z" does not exist in word.
You should not do any reverse operation, the resulting string is "abcd".
```
##### Constraints:
* 1 <= word.length <= 250
* word consists of lowercase English letters.
* ch is a lowercase English letter.

### Solution:
```java
class Solution {
    public String reversePrefix(String word, char ch) {
        StringBuffer sb = new StringBuffer();
        int n = word.length();
        int i = 0;
        for(; i < n; i++){
            char c = word.charAt(i);
            sb.append(c);
            if(c == ch) break;
        }
        
        if(i == n) return sb.toString();
        return sb.reverse().append(word.substring(i + 1,n)).toString();
    }
}
```