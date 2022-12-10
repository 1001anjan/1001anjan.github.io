---
layout: default
title: Find Words That Can Be Formed by Characters
parent: Data Structure Easy Set 6
grand_parent: Data Structure
nav_order: 15
permalink: /problem-175-Distance-Between-Bus-Stops/
---
# Find Words That Can Be Formed by Characters

You are given an array of strings words and a string chars.

A string is good if it can be formed by characters from chars (each character can only be used once).

Return the sum of lengths of all good strings in words.

##### Example 1:
```markdown
Input: words = ["cat","bt","hat","tree"], chars = "atach"
Output: 6
Explanation: The strings that can be formed are "cat" and "hat" so the answer is 3 + 3 = 6.
```
##### Example 2:
```markdown
Input: words = ["hello","world","leetcode"], chars = "welldonehoneyr"
Output: 10
Explanation: The strings that can be formed are "hello" and "world" so the answer is 5 + 5 = 10.
```
##### Constraints:
* 1 <= words.length <= 1000
* 1 <= words[i].length, chars.length <= 100
* words[i] and chars consist of lowercase English letters.

### Solution:
```java
class Solution {
    public int countCharacters(String[] words, String chars) {
        int total = 0;
        int[] count = new int[26];
        
        for(char c : chars.toCharArray())
            count[c-'a']++;
        
        for(String str : words){
            int[] temp = new int[26];
            for(char c : str.toCharArray()) temp[c-'a']++;
            int i = 0;
            for(; i < 26; i++)
                if(count[i]<temp[i]) break;
            if(i == 26) total += str.length();
        }
        
        return total;
    }
}
```