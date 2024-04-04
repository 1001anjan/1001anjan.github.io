---
layout: default
title: Consecutive Characters
parent: Easy Set 7
grand_parent: DSA Easy
nav_order: 26
permalink: /problem-216-Consecutive-Characters/
---
# Consecutive Characters
The power of the string is the maximum length of a non-empty substring that contains only one unique character.

Given a string s, return the power of s.

##### Example 1:
```markdown
Input: s = "leetcode"
Output: 2
Explanation: The substring "ee" is of length 2 with the character 'e' only.
```
##### Example 2:
```markdown
Input: s = "abbcccddddeeeeedcba"
Output: 5
Explanation: The substring "eeeee" is of length 5 with the character 'e' only.
```
##### Constraints:
* 1 <= s.length <= 500
* s consists of only lowercase English letters.

### Solution:
```java
class Solution {
    public int maxPower(String s) {
        int max = -1;
        int currMax = 1;
        for(int i = 1; i < s.length(); i++){
            if(s.charAt(i - 1) == s.charAt(i)){
                currMax++;
            }else{
                max = Math.max(max, currMax);
                currMax = 1;
            }
        }
        
        return Math.max(max, currMax);
    }
}
```
#### Faster in execution: 
```java
class Solution {
    public int maxPower(String s) {
        int max = -1;
        int currMax = 1;
        char prev = s.charAt(0);
        for(int i = 1; i < s.length(); i++){
            char now = s.charAt(i);
            if(prev == now){
                currMax++;
            }else{
                max = Math.max(max, currMax);
                currMax = 1;
            }
            prev = now;
        }
        
        return Math.max(max, currMax);
    }
}
```