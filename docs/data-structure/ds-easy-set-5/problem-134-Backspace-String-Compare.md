---
layout: default
title: Backspace String Compare
parent: Data Structure Easy Set 5
grand_parent: Data Structure
nav_order: 4
permalink: /problem-134-Backspace-String-Compare/
---
# Backspace String Compare

Given two strings s and t, return true if they are equal when both are typed into empty text editors. '#' means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

##### Example 1:
```markdown
Input: s = "ab#c", t = "ad#c"
Output: true
Explanation: Both s and t become "ac".
```
##### Example 2:
```markdown
Input: s = "ab##", t = "c#d#"
Output: true
Explanation: Both s and t become "".
```
##### Example 3:
```markdown
Input: s = "a#c", t = "b"
Output: false
Explanation: s becomes "c" while t becomes "b".
```
##### Constraints:
* 1 <= s.length, t.length <= 200
* s and t only contain lowercase letters and '#' characters.

### Solution:
```java
class Solution {
    public boolean backspaceCompare(String s, String t) {
        return processBackspace(s).equals(processBackspace(t));
    }
    
    public String processBackspace(String s){
        StringBuilder sb = new StringBuilder();
        int c = 0;
        for(int i = s.length()-1; i>=0; i--){
            if(s.charAt(i) != '#'){
                if(c>0){
                   c--; 
                }else{
                    sb.append(s.charAt(i));
                }
            }else{
               c++; 
            }
        }
        return sb.toString();
    }
}
```

```java
class Solution {
    public boolean backspaceCompare(String S, String T) {
        return build(S).equals(build(T));
    }

    public String build(String S) {
        Stack<Character> ans = new Stack();
        for (char c: S.toCharArray()) {
            if (c != '#')
                ans.push(c);
            else if (!ans.empty())
                ans.pop();
        }
        return String.valueOf(ans);
    }
}
```
 ```java
class Solution {
    public boolean backspaceCompare(String S, String T) {
        int i = S.length() - 1, j = T.length() - 1;
        int skipS = 0, skipT = 0;

        while (i >= 0 || j >= 0) { // While there may be chars in build(S) or build (T)
            while (i >= 0) { // Find position of next possible char in build(S)
                if (S.charAt(i) == '#') {skipS++; i--;}
                else if (skipS > 0) {skipS--; i--;}
                else break;
            }
            while (j >= 0) { // Find position of next possible char in build(T)
                if (T.charAt(j) == '#') {skipT++; j--;}
                else if (skipT > 0) {skipT--; j--;}
                else break;
            }
            // If two actual characters are different
            if (i >= 0 && j >= 0 && S.charAt(i) != T.charAt(j))
                return false;
            // If expecting to compare char vs nothing
            if ((i >= 0) != (j >= 0))
                return false;
            i--; j--;
        }
        return true;
    }
}
```