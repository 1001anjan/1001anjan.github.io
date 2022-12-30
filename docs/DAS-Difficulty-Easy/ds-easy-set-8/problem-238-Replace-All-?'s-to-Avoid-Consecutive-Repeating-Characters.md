---
layout: default
title: Replace All ?'s to Avoid Consecutive Repeating Characters
parent: Easy Set 8
grand_parent: DSA Easy Difficulty
nav_order: 18
permalink: /problem-238-Replace-All-?'s-to-Avoid-Consecutive-Repeating-Characters/
---
# Replace All ?'s to Avoid Consecutive Repeating Characters
Given a string s containing only lowercase English letters and the '?' character, convert all the '?' characters into lowercase letters such that the final string does not contain any consecutive repeating characters. You cannot modify the non '?' characters.

It is guaranteed that there are no consecutive repeating characters in the given string except for '?'.

Return the final string after all the conversions (possibly zero) have been made. If there is more than one solution, return any of them. It can be shown that an answer is always possible with the given constraints.

##### Example 1:
```markdown
Input: s = "?zs"
Output: "azs"
Explanation: There are 25 solutions for this problem. From "azs" to "yzs", all are valid. Only "z" is an invalid modification as the string will consist of consecutive repeating characters in "zzs".
```
##### Example 2:
```markdown
Input: s = "ubv?w"
Output: "ubvaw"
Explanation: There are 24 solutions for this problem. Only "v" and "w" are invalid modifications as the strings will consist of consecutive repeating characters in "ubvvw" and "ubvww".
```
##### Constraints:
* 1 <= s.length <= 100
* s consist of lowercase English letters and '?'.

### Solution:
```java
class Solution {
    public String modifyString(String s) {
        char[] chars = s.toCharArray();
        char prev = '1';
        
        for(int i = 0; i < chars.length; i++){
            if(chars[i] == '?'){
                chars[i] = getNewChar(prev,chars[(i + 1)%chars.length]);
            }
            prev = chars[i];
        }
        return new String(chars);
    }
    
    public char getNewChar(char prev, char next){
        int i = 0;
        int p =   prev - 'a';
        int n =   next - 'a';
        
        while(i < 26){
            if(i != p && i != n) break;
            i++;
        }
        return (char)('a' + i);
    }
}
```