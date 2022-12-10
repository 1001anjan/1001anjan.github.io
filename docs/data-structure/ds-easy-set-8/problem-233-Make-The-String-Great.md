---
layout: default
title: Make The String Great
parent: Data Structure Easy Set 8
grand_parent: Data Structure
nav_order: 13
permalink: /problem-233-Make-The-String-Great/
---
# Make The String Great
Given a string s of lower and upper case English letters.

A good string is a string which doesn't have two adjacent characters s[i] and s[i + 1] where:

* 0 <= i <= s.length - 2
* s[i] is a lower-case letter and s[i + 1] is the same letter but in upper-case or vice-versa.

To make the string good, you can choose two adjacent characters that make the string bad and remove them. You can keep doing this until the string becomes good.

Return the string after making it good. The answer is guaranteed to be unique under the given constraints.

Notice that an empty string is also good.

##### Example 1:
```markdown
Input: s = "leEeetcode"
Output: "leetcode"
Explanation: In the first step, either you choose i = 1 or i = 2, both will result "leEeetcode" to be reduced to "leetcode".
```
##### Example 2:
```markdown
Input: s = "abBAcC"
Output: ""
Explanation: We have many possible scenarios, and all lead to the same answer. For example:
"abBAcC" --> "aAcC" --> "cC" --> ""
"abBAcC" --> "abBA" --> "aA" --> ""
```
##### Example 3:
```markdown
Input: s = "s"
Output: "s"
```
##### Constraints:
* 1 <= s.length <= 100
* s contains only lower and upper case English letters.

### Solution:
```java
class Solution {
    public String makeGood(String s) {
        StringBuilder sb = new StringBuilder();
        boolean status = false;
        sb.append(s);
        while(!status ){
            char[] chs = sb.toString().toCharArray();
            sb.setLength(0);
            status = true;
            for(int i = 0; i < chs.length; i++){
                if(i < chs.length - 1 
                   && chs[i] != chs[i+1] 
                   && Character.toUpperCase(chs[i]) == Character.toUpperCase(chs[i+1])){
                    i++;
                    status = false;
                }else{
                    sb.append(chs[i]);
                }
            }
        }
        return sb.toString();
    }
}
```
#### Using recursion
```java
class Solution {
    public String makeGood(String s) {
        
        for(int i=0;i<s.length() - 1;i++){
            if(Math.abs(s.charAt(i) - s.charAt(i+1)) ==32)
                return makeGood(s.substring(0, i)+ s.substring(i+2));
        }   
         
        return s;
    }
}
```
#### using Stack but slow approach
```java
class Solution {
    public String makeGood(String s) {
        Stack<Character> stk = new Stack<>();
        
		for(int i=0; i<s.length(); i++){
            char c = s.charAt(i);
            if(!stk.isEmpty() && Math.abs(stk.peek()-c) == 32)
                stk.pop();
            else 
                stk.push(c);
        }
        
        StringBuilder res = new StringBuilder();
        while(!stk.isEmpty())
            res.append(stk.pop());
        
        return res.reverse().toString();
    }
}
```