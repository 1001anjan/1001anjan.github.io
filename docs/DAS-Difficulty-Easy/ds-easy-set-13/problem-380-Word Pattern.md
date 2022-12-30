---
layout: default
title: Word Pattern
parent: Easy Set 13
grand_parent: DSA Easy Difficulty
nav_order: 10
permalink: /problem-380-Word Pattern/
---
# Word Pattern
Given a pattern and a string s, find if s follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in s.

##### Example 1:
```markdown
Input: pattern = "abba", s = "dog cat cat dog"
Output: true
```
##### Example 2:
```markdown
Input: pattern = "abba", s = "dog cat cat fish"
Output: false
```
##### Example 3:
```markdown
Input: pattern = "aaaa", s = "dog cat cat dog"
Output: false
```
##### Constraints:
* 1 <= pattern.length <= 300
* pattern contains only lower-case English letters.
* 1 <= s.length <= 3000
* s contains only lowercase English letters and spaces ' '.
* s does not contain any leading or trailing spaces.
* All the words in s are separated by a single space.

### Solution:
```java
class Solution {
    public boolean wordPattern(String pattern, String s) {
        String[] str = s.split(" ");
        if(pattern.length()!=str.length) return false;

        HashMap<Character, String> hm = new HashMap<>();
        for(int i=0; i<pattern.length(); i++){
            char c = pattern.charAt(i);
            if(hm.containsKey(c)){
                if(!hm.get(c).equals(str[i]))return false;
            } else{
                if(hm.containsValue(str[i])) return false;
                hm.put(c, str[i]);
            }
        }
        return true;
    }
}

```