---
layout: default
title: Remove Outermost Parentheses
parent: Easy Set 14
grand_parent: DSA Easy
nav_order: 6
permalink: /problem-406-Remove Outermost Parentheses/
---
# Remove Outermost Parentheses
A valid parentheses string is either empty "", "(" + A + ")", or A + B, where A and B are valid parentheses strings, and + represents string concatenation.

* For example, "", "()", "(())()", and "(()(()))" are all valid parentheses strings.

A valid parentheses string s is primitive if it is nonempty, and there does not exist a way to split it into s = A + B, with A and B nonempty valid parentheses strings.

Given a valid parentheses string s, consider its primitive decomposition: s = P1 + P2 + ... + Pk, where Pi are primitive valid parentheses strings.

Return s after removing the outermost parentheses of every primitive string in the primitive decomposition of s.

##### Example 1:
```markdown
Input: s = "(()())(())"
Output: "()()()"
Explanation:
The input string is "(()())(())", with primitive decomposition "(()())" + "(())".
After removing outer parentheses of each part, this is "()()" + "()" = "()()()".
```
##### Example 2:
```markdown
Input: s = "(()())(())(()(()))"
Output: "()()()()(())"
Explanation:
The input string is "(()())(())(()(()))", with primitive decomposition "(()())" + "(())" + "(()(()))".
After removing outer parentheses of each part, this is "()()" + "()" + "()(())" = "()()()()(())".
```
##### Example 3:
```markdown
Input: s = "()()"
Output: ""
Explanation:
The input string is "()()", with primitive decomposition "()" + "()".
After removing outer parentheses of each part, this is "" + "" = "".
```
##### Constraints:
* 1 <= s.length <= 105
* s[i] is either '(' or ')'.
* s is a valid parentheses string.

### Solution:
```java
class Solution {
    public String removeOuterParentheses(String s) {
        int open = 0;
        StringBuilder sb = new StringBuilder();
        for(char ch : s.toCharArray()){
            if(ch == '('){
                if(open == 0){
                    open++;
                }else{
                    open++;
                    sb.append(ch);
                }
            }else{
                if(open > 1){
                    open--;
                    sb.append(ch);
                }else{
                    open = 0;
                }
            }
        }
        
        return sb.toString();
    }
}
```
```java
class Solution {
    public String removeOuterParentheses(String S) {
        StringBuilder s = new StringBuilder();
        int opened = 0;
        for (char c : S.toCharArray()) {
            if (c == '(' && opened++ > 0) s.append(c);
            if (c == ')' && opened-- > 1) s.append(c);
        }
        return s.toString();
    }
}
```