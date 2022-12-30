---
layout: default
title: Buddy Strings
parent: Easy Set 5
grand_parent: DSA Easy Difficulty
nav_order: 5
permalink: /problem-135-Buddy-Strings/
---
# Buddy Strings

Given two strings s and goal, return true if you can swap two letters in s so the result is equal to goal, otherwise, return false.

Swapping letters is defined as taking two indices i and j (0-indexed) such that i != j and swapping the characters at s[i] and s[j].

For example, swapping at indices 0 and 2 in "abcd" results in "cbad".

##### Example 1:
```markdown
Input: s = "ab", goal = "ba"
Output: true
Explanation: You can swap s[0] = 'a' and s[1] = 'b' to get "ba", which is equal to goal.
```
##### Example 2:
```markdown
Input: s = "ab", goal = "ab"
Output: false
Explanation: The only letters you can swap are s[0] = 'a' and s[1] = 'b', which results in "ba" != goal.
```
##### Example 3:
```markdown
Input: s = "aa", goal = "aa"
Output: true
Explanation: You can swap s[0] = 'a' and s[1] = 'a' to get "aa", which is equal to goal.
```
##### Constraints:
* 1 <= s.length, goal.length <= 2 * 104
* s and goal consist of lowercase letters.

### Solution:
```java
class Solution {
    public boolean buddyStrings(String s, String goal) {
        if(s.length() != goal.length()) return false;
        if(s.equals(goal)){
            int[] arr = new int[26];
            for(char c: s.toCharArray()){
                arr[c-'a']++;
            }
            for(int i=0; i<26;i++){
                if(arr[i]>1) return true;
            }
            return false;
        }else{
            int first = -1;
            int second = -1;
            for(int i=0; i<s.length(); i++){
                if(s.charAt(i) != goal.charAt(i)){
                    if(first == -1) first = i;
                    else if(second == -1) second = i;
                    else return false;
                }
            }
            if(second == -1) return false;
            return s.charAt(first) == goal.charAt(second) && s.charAt(second) == goal.charAt(first);
        }
    }
}
```