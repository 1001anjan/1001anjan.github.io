---
layout: default
title: Evaluate Reverse Polish Notation
parent: Medium Set 2
grand_parent: DSA Medium
nav_order: 27
permalink: /problem-77-Evaluate Reverse Polish Notation/
---
# Evaluate Reverse Polish Notation
Evaluate the value of an arithmetic expression in Reverse Polish Notation.

Valid operators are +, -, *, and /. Each operand may be an integer or another expression.

Note that division between two integers should truncate toward zero.

It is guaranteed that the given RPN expression is always valid. That means the expression would always evaluate to a result, and there will not be any division by zero operation.

##### Example 1:
```markdown
Input: tokens = ["2","1","+","3","*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
```
##### Example 2:
```markdown
Input: tokens = ["4","13","5","/","+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
```
##### Example 3:
```markdown
Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
Output: 22
Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```
##### Constraints:
* 1 <= tokens.length <= 10^4
* tokens[i] is either an operator: "+", "-", "*", or "/", or an integer in the range [-200, 200].

### Solution:
```java
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> s = new Stack<>();
        for(String str : tokens){
            switch(str){
                case "+" : s.push(s.pop() + s.pop()); break;
                case "-" : int a = s.pop(); int b = s.pop(); s.push(b - a); break;
                case "*" : s.push(s.pop() * s.pop()); break;
                case "/" : a = s.pop();  b = s.pop(); s.push(b/a); break;
                default  : s.push(Integer.parseInt(str));
            }
        }
        return s.pop();
    }
}
```