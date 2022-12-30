---
layout: default
title: Greatest English Letter in Upper and Lower Case
parent: Easy Set 12
grand_parent: DSA Easy Difficulty
nav_order: 21
permalink: /problem-361-Greatest English Letter in Upper and Lower Case/
---
# Greatest English Letter in Upper and Lower Case
Given a string of English letters s, return the greatest English letter which occurs as both a lowercase and uppercase letter in s. The returned letter should be in uppercase. If no such letter exists, return an empty string.

An English letter b is greater than another letter a if b appears after a in the English alphabet.

##### Example 1:
```markdown
Input: s = "lEeTcOdE"
Output: "E"
Explanation:
The letter 'E' is the only letter to appear in both lower and upper case.
```
##### Example 2:
```markdown
Input: s = "arRAzFif"
Output: "R"
Explanation:
The letter 'R' is the greatest letter to appear in both lower and upper case.
Note that 'A' and 'F' also appear in both lower and upper case, but 'R' is greater than 'F' or 'A'.
```
##### Example 3:
```markdown
Input: s = "AbCdEfGhIjK"
Output: ""
Explanation:
There is no letter that appears in both lower and upper case.
```
##### Constraints:
* 1 <= s.length <= 1000
* s consists of lowercase and uppercase English letters.

### Solution:
```java
class Solution {
    public String greatestLetter(String s) {
        boolean[][] cm = new boolean[26][2];
        for(char c : s.toCharArray()){
            if(Character.isUpperCase(c)){
                cm[c - 'A'][0] = true;
            }else{
                cm[c - 'a'][1] = true;
            }
        }

        for(int i = 25; i >= 0; i--){
            if(cm[i][0] && cm[i][1]) return Character.toString('A' + i);
        }
        return "";
    }
}
```
##### Improvement
```java
class Solution {
    public String greatestLetter(String s) {
        boolean[] letters = new boolean[58];
        for (char c : s.toCharArray()) {
            letters[c - 'A'] = true;
        }
        for (int i = 26; i >= 0; i--) {
            if (letters[i] && letters[i + 32]) {
                return "" + (char)('A' + i);
            }
        }
        return "";
    }
}
```