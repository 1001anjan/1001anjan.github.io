---
layout: default
title: Reverse Only Letters
parent: Easy Set 5
grand_parent: DSA Easy Difficulty
nav_order: 15
permalink: /problem-145-Reverse-Only-Letters/
---
# Reverse Only Letters

Given a string s, reverse the string according to the following rules:

All the characters that are not English letters remain in the same position.
All the English letters (lowercase or uppercase) should be reversed.
Return s after reversing it.

##### Example 1:
```markdown
Input: s = "ab-cd"
Output: "dc-ba"
```
##### Example 2:
```markdown
Input: s = "a-bC-dEf-ghIj"
Output: "j-Ih-gfE-dCba"
```
##### Example 3:
```markdown
Input: s = "Test1ng-Leet=code-Q!"
Output: "Qedo1ct-eeLg=ntse-T!"
```
##### Constraints:
* 1 <= s.length <= 100
* s consists of characters with ASCII values in the range [33, 122].
* s does not contain '\"' or '\\'.

### Solution:
```java
class Solution {
    public String reverseOnlyLetters(String str) {
        char[] chars = str.toCharArray();
        int s = 0;
        int e = chars.length - 1;
        while(s<e){
            // find letters left to right
            while(s<e && !Character.isLetter(chars[s])) s++;
            // find letters right to left
            while(s<e && !Character.isLetter(chars[e])) e--;
            if(s<e){
                char c = chars[s];
                chars[s] = chars[e];
                chars[e] = c;
            }
            s++;
            e--;
        }
        return new String(chars);
    }
}
```