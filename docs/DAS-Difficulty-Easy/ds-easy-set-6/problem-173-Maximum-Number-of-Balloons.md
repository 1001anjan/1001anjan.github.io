---
layout: default
title: Maximum Number of Balloons
parent: Easy Set 6
grand_parent: DSA Easy Difficulty
nav_order: 13
permalink: /problem-173-Maximum-Number-of-Balloons/
---
# Maximum Number of Balloons

Given a string text, you want to use the characters of text to form as many instances of the word "balloon" as possible.

You can use each character in text at most once. Return the maximum number of instances that can be formed.

##### Example 1:
```markdown
Input: text = "nlaebolko"
Output: 1
```
##### Example 2:
```markdown
Input: text = "loonbalxballpoon"
Output: 2
```
##### Example 3:
```markdown
Input: text = "leetcode"
Output: 0
```
##### Constraints:
* 1 <= text.length <= 104
* text consists of lower case English letters only.

### Solution:
```java
class Solution {
    public int maxNumberOfBalloons(String text) {
        Map<Character,Integer> m = new HashMap<>();
        for(char c : text.toCharArray())
            if(c == 'b' || c == 'a' || c == 'n' || c == 'l' || c == 'o') m.put(c,m.getOrDefault(c,0)+1);
        
        if(m.size() != 5) return 0;
        
        int max = m.get('b');
        for(char c : m.keySet()){
            if(c == 'l' || c == 'o')
                max = Math.min(max, m.get(c)/2);
            else max = Math.min(max, m.get(c));
        }
        return max;
    }
}
```