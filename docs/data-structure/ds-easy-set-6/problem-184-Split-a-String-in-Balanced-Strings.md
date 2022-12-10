---
layout: default
title: Split a String in Balanced Strings
parent: Data Structure Easy Set 6
grand_parent: Data Structure
nav_order: 24
permalink: /problem-184-Split-a-String-in-Balanced-Strings/
---
# Split a String in Balanced Strings

Balanced strings are those that have an equal quantity of 'L' and 'R' characters.

Given a balanced string s, split it into some number of substrings such that:

Each substring is balanced.
Return the maximum number of balanced strings you can obtain.

##### Example 1:
```markdown
Input: s = "RLRRLLRLRL"
Output: 4
Explanation: s can be split into "RL", "RRLL", "RL", "RL", each substring contains same number of 'L' and 'R'.
```
##### Example 2:
```markdown
Input: s = "RLRRRLLRLL"
Output: 2
Explanation: s can be split into "RL", "RRRLLRLL", each substring contains same number of 'L' and 'R'.
Note that s cannot be split into "RL", "RR", "RL", "LR", "LL", because the 2nd and 5th substrings are not balanced.
```
##### Example 3:
```markdown
Input: s = "LLLLRRRR"
Output: 1
Explanation: s can be split into "LLLLRRRR".
```
##### Constraints:
* 2 <= s.length <= 1000
* s[i] is either 'L' or 'R'.
* s is a balanced string.

### Solution:
```java
class Solution {
    public int balancedStringSplit(String s) {
        int count = 0;
        int c = 0;
        for(char ch : s.toCharArray()){
            if( ch == 'L') 
                count++;
            else
                count--;
            
            if(count == 0){
                c++;
            }
        }
        return c;
    }
}
```