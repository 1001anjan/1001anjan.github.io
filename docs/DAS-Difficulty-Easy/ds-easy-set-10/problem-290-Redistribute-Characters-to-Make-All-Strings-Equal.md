---
layout: default
title: Redistribute Characters to Make All Strings Equal
parent: Easy Set 10
grand_parent: DSA Easy Difficulty
nav_order: 10
permalink: /problem-290-Redistribute-Characters-to-Make-All-Strings-Equal/
---
# Redistribute Characters to Make All Strings Equal
You are given an array of strings words (0-indexed).

In one operation, pick two distinct indices i and j, where words[i] is a non-empty string, and move any character from words[i] to any position in words[j].

Return true if you can make every string in words equal using any number of operations, and false otherwise.

##### Example 1:
```markdown
Input: words = ["abc","aabc","bc"]
Output: true
Explanation: Move the first 'a' in words[1] to the front of words[2],
to make words[1] = "abc" and words[2] = "abc".
All the strings are now equal to "abc", so return true.
```
##### Example 2:
```markdown
Input: words = ["ab","a"]
Output: false
Explanation: It is impossible to make all the strings equal using the operation.
```
##### Constraints:
* 1 <= words.length <= 100
* 1 <= words[i].length <= 100
* words[i] consists of lowercase English letters.

### Solution
```java
class Solution {
    public boolean makeEqual(String[] words) {
        int[] count = new int[26];
        for(String w : words){
            for(char c : w.toCharArray()){
                count[c - 'a']++;
            }
        }
        for(int i : count){
            if(i % words.length != 0) return false;
        }
        
        return true;
    }
}
```