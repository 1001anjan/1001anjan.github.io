---
layout: default
title: Length of Last Word
parent: Data Structure Easy Set 1
grand_parent: Data Structure
nav_order: 12
permalink: /problem-12-length-of-last-word/
---
# Length of Last Word

Given a string s consisting of words and spaces, return the length of the last word in the string.

A word is a maximal substring consisting of non-space characters only.

#### Example 1:
```markdown
Input: s = "Hello World"
Output: 5
Explanation: The last word is "World" with length 5.
```
#### Example 2:
```markdown
Input: s = "   fly me   to   the moon  "
Output: 4
Explanation: The last word is "moon" with length 4.
```
#### Example 3:
```markdown
Input: s = "luffy is still joyboy"
Output: 6
Explanation: The last word is "joyboy" with length 6.
```

### Constraints:

* 1 <= s.length <= 104
* s consists of only English letters and spaces ' '.
* There will be at least one word in s.

### Solution
```java
class Solution {
    public int lengthOfLastWord(String s) {
        int l = 0;
        s = s.trim();
        for(int i = s.length()-1; i>=0; i--){
            if(s.charAt(i) == ' ') break;
            l++;
        }
        return l;
    }
}
```