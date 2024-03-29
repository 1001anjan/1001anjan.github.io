---
layout: default
title: Percentage of Letter in String
parent: Easy Set 12
grand_parent: DSA Easy
nav_order: 16
permalink: /problem-356-Percentage of Letter in String/
---
# Percentage of Letter in String
Given a string s and a character letter, return the percentage of characters in s that equal letter rounded down to the nearest whole percent.

##### Example 1:
```markdown
Input: s = "foobar", letter = "o"
Output: 33
Explanation:
The percentage of characters in s that equal the letter 'o' is 2 / 6 * 100% = 33% when rounded down, so we return 33.
```
##### Example 2:
```markdown
Input: s = "jjjj", letter = "k"
Output: 0
Explanation:
The percentage of characters in s that equal the letter 'k' is 0%, so we return 0.
```
##### Constraints:
* 1 <= s.length <= 100
* s consists of lowercase English letters.
* letter is a lowercase English letter.

### Solution:
```java
class Solution {
    public int percentageLetter(String s, char letter) {
        int c = 0;
        for(char ch : s.toCharArray()) 
            if(ch == letter) c++;
        return (c * 100) / s.length();
    }
}
```