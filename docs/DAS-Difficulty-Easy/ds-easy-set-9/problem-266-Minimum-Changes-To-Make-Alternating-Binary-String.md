---
layout: default
title: Minimum Changes To Make Alternating Binary String
parent: Easy Set 9
grand_parent: DSA Easy
nav_order: 16
permalink: /problem-266-Minimum-Changes-To-Make-Alternating-Binary-String/
---
# Minimum Changes To Make Alternating Binary String
You are given a string s consisting only of the characters '0' and '1'. In one operation, you can change any '0' to '1' or vice versa.

The string is called alternating if no two adjacent characters are equal. For example, the string "010" is alternating, while the string "0100" is not.

Return the minimum number of operations needed to make s alternating.

##### Example 1:
```markdown
Input: s = "0100"
Output: 1
Explanation: If you change the last character to '1', s will be "0101", which is alternating.
```
##### Example 2:
```markdown
Input: s = "10"
Output: 0
Explanation: s is already alternating.
```
##### Example 3:
```markdown
Input: s = "1111"
Output: 2
Explanation: You need two operations to reach "0101" or "1010".
```
##### Constraints:
* 1 <= s.length <= 10^4
* s[i] is either '0' or '1'.

### Solution:
```java
class Solution {
    public int minOperations(String s) {
        int c1, c2;
        c1 = c2 = 0;
        boolean stc = true;
        for(char c : s.toCharArray()){
            if(stc){
                if(c == '0') 
                    c2++; 
                else
                    c1++;
            }else{
                if(c == '0') 
                    c1++;
                else
                   c2++; 
            }
            stc = !stc;
        }
        return Math.min(c1,c2);
    }
}
```
