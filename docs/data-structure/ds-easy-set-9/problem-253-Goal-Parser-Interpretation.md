---
layout: default
title: Goal Parser Interpretation
parent: Data Structure Easy Set 9
grand_parent: Data Structure
nav_order: 3
permalink: /problem-253-Goal-Parser Interpretation/
---
# Goal Parser Interpretation
You own a Goal Parser that can interpret a string command. The command consists of an alphabet of "G", "()" and/or "(al)" in some order. The Goal Parser will interpret "G" as the string "G", "()" as the string "o", and "(al)" as the string "al". The interpreted strings are then concatenated in the original order.

Given the string command, return the Goal Parser's interpretation of command.

##### Example 1:
```markdown
Input: command = "G()(al)"
Output: "Goal"
Explanation: The Goal Parser interprets the command as follows:
G -> G
() -> o
(al) -> al
The final concatenated result is "Goal".
```
##### Example 2:
```markdown
Input: command = "G()()()()(al)"
Output: "Gooooal"
```
##### Example 3:
```markdown
Input: command = "(al)G(al)()()G"
Output: "alGalooG"
```
##### Constraints:
* 1 <= command.length <= 100
* command consists of "G", "()", and/or "(al)" in some order.

### Solution:
```java
class Solution {
    public String interpret(String command) {
        StringBuilder sb = new StringBuilder();
        char[] s = command.toCharArray();
        int i = 0;
        while(i < s.length){
            if(s[i] == 'G'){
                sb.append("G");
                i++;
            }else if(s[i] == '('){
                if(s[i + 1] == ')'){
                    sb.append("o");
                    i = i+ 2;
                }else{
                    i++;
                    while(s[i] != ')') sb.append(s[i++]);
                    i++;
                }
            }
        }
        return sb.toString();
    }
}
```