---
layout: default
title: Largest Substring Between Two Equal Characters
parent: Data Structure Easy Set 8
grand_parent: Data Structure
nav_order: 26
permalink: /problem-246-Largest-Substring-Between-Two-Equal-Characters/
---
# Largest Substring Between Two Equal Characters

Given a string s, return the length of the longest substring between two equal characters, excluding the two characters. If there is no such substring return -1.

A substring is a contiguous sequence of characters within a string.

##### Example 1:
```markdown
Input: s = "aa"
Output: 0
Explanation: The optimal substring here is an empty substring between the two 'a's.
```
##### Example 2:
```markdown
Input: s = "abca"
Output: 2
Explanation: The optimal substring here is "bc".
```
##### Example 3:
```markdown
Input: s = "cbzxy"
Output: -1
Explanation: There are no characters that appear twice in s.
```
##### Constraints:
* 1 <= s.length <= 300
* s contains only lowercase English letters.

### Solution:
```java
class Solution {
    public int maxLengthBetweenEqualCharacters(String s) {
        int[][] index = new int[26][2];
        
        for(int i = 0; i < s.length(); i++){
            char c = s.charAt(i);
            if(index[c - 'a'][0] == 0) 
                index[c - 'a'][0] = i + 1;
            else
                index[c - 'a'][1] = i + 1;
        }
        
        int max = index[0][1] - index[0][0] - 1;
        
        for(int i = 1; i < 26; i++){
            max = Math.max(max, index[i][1] - index[i][0] - 1);
        }
        
        return max;
    }
}
```

####  O(n*n) Time complexity
```java
class Solution {
    public int maxLengthBetweenEqualCharacters(String s) {
        int res = -1;
        for(int i=0; i<s.length(); i++){
            char c = s.charAt(i);
            res = Math.max(res, s.lastIndexOf(c) - s.indexOf(c)-1);            
        }
        return res;
    }
}
```