---
layout: default
title: Valid Parentheses
parent: Data Structure Easy Set 1
grand_parent: Data Structure
nav_order: 5
permalink: /problem-5-valid-parentheses/
---

# Valid Parentheses

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.


### Example 1:
```markdown
Input: s = "()"
Output: true
```
### Example 2:
```markdown
Input: s = "()[]{}"
Output: true
```
### Example 3:
```markdown
Input: s = "(]"
Output: false
```

### Constraints:

* 1 <= s.length <= 104
* s consists of parentheses only '()[]{}'.

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack();
        
        for(int i = 0; i<s.length(); i++){
            if(s.charAt(i) == '(' || s.charAt(i) == '{' || s.charAt(i) == '['){
                stack.push(s.charAt(i));
            }else{
                if(stack.isEmpty()) return false;
                if(s.charAt(i) != getCorrospondingBracket(stack.pop())) return false;
            }
        }
        if(stack.isEmpty()) return true;
        return false;
    }
    
    private char getCorrospondingBracket(char c){
        switch(c){
            case '(': return ')';
            case '{': return '}';
            case '[': return ']';
            default : return '*';
        }
    }
}
```