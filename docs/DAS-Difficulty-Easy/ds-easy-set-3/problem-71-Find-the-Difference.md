---
layout: default
title: Find the Difference
parent: Easy Set 3
grand_parent: DSA Easy
nav_order: 8
permalink: /problem-71-Find-the-Difference/
---
# Find the Difference
You are given two strings s and t.

String t is generated by random shuffling string s and then add one more letter at a random position.

Return the letter that was added to t.

##### Example 1:
```markdown
Input: s = "abcd", t = "abcde"
Output: "e"
Explanation: 'e' is the letter that was added.
```
##### Example 2:
```markdown
Input: s = "", t = "y"
Output: "y"
```
##### Constraints:
* 0 <= s.length <= 1000
* t.length == s.length + 1
* s and t consist of lowercase English letters.

### Solution
```java
class Solution {
    public char findTheDifference(String s, String t) {
        int ch[] = new int[26];
        for(int i=0; i<t.length(); i++){
            ch[t.charAt(i) - 'a']++;
        }
        for(int i=0; i<s.length(); i++){
            ch[s.charAt(i) - 'a']--;
        }
        for(int i = 0; i<26; i++){
            if(ch[i] == 1) return (char)('a'+i);
        }
        return '1';
    }
}
```
###### Using XOR
```java
class Solution {
    public char findTheDifference(String s, String t) {
        char res = 0;

        for(char ch: s.toCharArray()) {
            res ^= ch;
        }

        for(char ch: t.toCharArray()) {
            res ^= ch;
        }

        return res;
    }
}
```