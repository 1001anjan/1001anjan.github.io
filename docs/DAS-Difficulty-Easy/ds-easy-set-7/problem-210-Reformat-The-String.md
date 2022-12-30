---
layout: default
title: Reformat The String
parent: Easy Set 7
grand_parent: DSA Easy Difficulty
nav_order: 20
permalink: /problem-210-Reformat-The-String/
---
# Reformat The String
You are given an alphanumeric string s. (Alphanumeric string is a string consisting of lowercase English letters and digits).

You have to find a permutation of the string where no letter is followed by another letter and no digit is followed by another digit. That is, no two adjacent characters have the same type.

Return the reformatted string or return an empty string if it is impossible to reformat the string.

##### Example 1:
```markdown
Input: s = "a0b1c2"
Output: "0a1b2c"
Explanation: No two adjacent characters have the same type in "0a1b2c". "a0b1c2", "0a1b2c", "0c2a1b" are also valid permutations.
```
##### Example 2:
```markdown
Input: s = "leetcode"
Output: ""
Explanation: "leetcode" has only characters so we cannot separate them by digits.
```

##### Example 3:
```markdown
Input: s = "1229857369"
Output: ""
Explanation: "1229857369" has only digits so we cannot separate them by characters.
```
##### Constraints:
* 1 <= s.length <= 500
* s consists of only lowercase English letters and/or digits.

```java
class Solution {
    public String reformat(String s) {
        int letters = 0, numbers = 0;
        for(char c : s.toCharArray()){
            if(Character.isDigit(c)) numbers++;
            else letters++;
        }
        
        if(Math.abs(letters - numbers) > 1) return "";
        return letters > numbers ? makeResult(s,0,1) : makeResult(s,1,0);
    }
    
    private String makeResult(String s, int i, int j){
        char[] c = s.toCharArray();
        char[] res = new char[s.length()];
        for(char ch: c){
            if(Character.isLetter(ch)){
                res[i] = ch;
                i+=2;
            }else{
                res[j] = ch;
                j+=2;
            }
        }
        return String.valueOf(res);
    }
}
```