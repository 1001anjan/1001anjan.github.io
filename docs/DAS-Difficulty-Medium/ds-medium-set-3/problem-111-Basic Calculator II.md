---
layout: default
title: Basic Calculator II
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 11
permalink: /problem-111-Basic Calculator II/
---
# Basic Calculator II
Given a string s which represents an expression, evaluate this expression and return its value.

The integer division should truncate toward zero.

You may assume that the given expression is always valid. All intermediate results will be in the range of [-2^31, 2^31 - 1].

Note: You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as eval().

##### Example 1:
```markdown
Input: s = "3+2*2"
Output: 7
```
##### Example 2:
```markdown
Input: s = " 3/2 "
Output: 1
```
##### Example 3:
```markdown
Input: s = " 3+5 / 2 "
Output: 5
```
##### Constraints:
* 1 <= s.length <= 3 * 10^5
* s consists of integers and operators ('+', '-', '*', '/') separated by some number of spaces.
* s represents a valid expression.
* All the integers in the expression are non-negative integers in the range [0, 2^31 - 1].
* The answer is guaranteed to fit in a 32-bit integer.

### Solution:
```java
class Solution {
    public int calculate(String s) {
        char prevOp = '+';  // previous operator 
        int prevValue = 0;  // previous number
        int result = 0;    // total result
        int value = 0;  // current value 

        int i = 0;
        int len = s.length();
        while(i < len){
            
            if(s.charAt(i) == ' '){
                i++;
                continue;
            }
            char ch = s.charAt(i);

            while(Character.isDigit(ch)){
                value = value * 10 + ch - '0';
                i++;
                if(i >= len) break;
                ch = s.charAt(i);
            }
            switch(prevOp){
                case '+':   result += prevValue;
                            prevValue = value;
                            break;
                case '-':   result += prevValue; 
                            prevValue = -value;
                            break;
                case '*':   prevValue = prevValue * value;
                            break;
                case '/':   prevValue = prevValue / value; 
                            break;
            }
            i++;
            prevOp = ch;
            value = 0;
        }

        return result + prevValue;
    }
}
```