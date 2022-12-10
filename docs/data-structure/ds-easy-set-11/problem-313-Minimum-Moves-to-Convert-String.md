---
layout: default
title: Minimum Moves to Convert String
parent: Data Structure Easy Set 11
grand_parent: Data Structure
nav_order: 3
permalink: /problem-313-Minimum Moves to Convert String/
---
# Minimum Moves to Convert String
You are given a string s consisting of n characters which are either 'X' or 'O'.

A move is defined as selecting three consecutive characters of s and converting them to 'O'. Note that if a move is applied to the character 'O', it will stay the same.

Return the minimum number of moves required so that all the characters of s are converted to 'O'.

##### Example 1:
```markdown
Input: s = "XXX"
Output: 1
Explanation: XXX -> OOO
We select all the 3 characters and convert them in one move.
```
##### Example 2:
```markdown
Input: s = "XXOX"
Output: 2
Explanation: XXOX -> OOOX -> OOOO
We select the first 3 characters in the first move, and convert them to 'O'.
Then we select the last 3 characters and convert them so that the final string contains all 'O's.
```
##### Example 3:
```markdown
Input: s = "OOOO"
Output: 0
Explanation: There are no 'X's in s to convert.
```
##### Constraints:
* 3 <= s.length <= 1000
* s[i] is either 'X' or 'O'.

### Solution:
```java
class Solution {
    public int minimumMoves(String s) {
        int count = 0;
        int idx = 0;
        while(idx < s.length()){
            if(s.charAt(idx) == 'O'){ // if we hit a 'O' we can skip it 
                idx++;
            }else{
                count++; // we find a 'X'
                idx += 3; // we will flip the substing from(idx, idx+3);  
            }

        }
        return count;
    }
}
```