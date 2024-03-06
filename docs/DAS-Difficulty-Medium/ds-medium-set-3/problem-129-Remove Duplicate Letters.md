---
layout: default
title: Remove Duplicate Letters
parent: Medium Set 3
grand_parent: DSA Medium
nav_order: 29
permalink: /problem-129-Remove Duplicate Letters/
---
# Remove Duplicate Letters
Given a string s, remove duplicate letters so that every letter appears once and only once. You must make sure your result is the smallest in lexicographical order among all possible results.

##### Example 1:
```markdown
Input: s = "bcabc"
Output: "abc"
```
##### Example 2:
```markdown
Input: s = "cbacdcbc"
Output: "acdb"
```
##### Constraints:
* 1 <= s.length <= 10^4
* s consists of lowercase English letters.

### Solution:
```java
class Solution {
    public String removeDuplicateLetters(String s) {
        Stack<Character> stack = new Stack<>();
        int[] lastIndex = new int[26];
        int len = s.length();

        for(int i = 0; i < len; i++){
            lastIndex[s.charAt(i) - 'a'] = i;
        }

        Set<Character> seen = new HashSet<>();
        stack.push(s.charAt(0));
        seen.add(stack.peek());
        for(int i = 1; i < len; i++){
            char ch = s.charAt(i);
            if(seen.contains(ch)) continue;

            while(!stack.isEmpty()){
                char c = stack.peek();
                if(c > ch && lastIndex[c - 'a'] > i){
                    stack.pop();
                    seen.remove(c);
                }else{
                    break;
                }
            }
            seen.add(ch);
            stack.push(ch);
        }

        StringBuilder sb = new StringBuilder();
        while(!stack.isEmpty()) sb.append(stack.pop());
        return sb.reverse().toString();
    }
}
```