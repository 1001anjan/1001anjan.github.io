---
layout: default
title: Jewels and Stones
parent: Data Structure Easy Set 13
grand_parent: Data Structure
nav_order: 23
permalink: /problem-393-Jewels and Stones/
---
# Jewels and Stones
You're given strings jewels representing the types of stones that are jewels, and stones representing the stones you have. Each character in stones is a type of stone you have. You want to know how many of the stones you have are also jewels.

Letters are case sensitive, so "a" is considered a different type of stone from "A".

##### Example 1:
```markdown
Input: jewels = "aA", stones = "aAAbbbb"
Output: 3
```
##### Example 2:
```markdown
Input: jewels = "z", stones = "ZZ"
Output: 0
```
##### Constraints:
* 1 <= jewels.length, stones.length <= 50
* jewels and stones consist of only English letters.
* All the characters of jewels are unique.

### Solution:
```java
class Solution {
    public int numJewelsInStones(String jewels, String stones) {
        int count = 0;
        boolean[] um = new boolean[26];
        boolean[] lm = new boolean[26];
        
        for(char ch : jewels.toCharArray()){
            if(Character.isUpperCase(ch)){
                um[ch - 'A'] = true;
            }else{
                lm[ch - 'a'] = true;
            }
        }
        
        for(char ch : stones.toCharArray()){
            if(Character.isUpperCase(ch)){
                if(um[ch - 'A']) count++;
            }else{
                if(lm[ch - 'a']) count++;
            }
        }
        
        return count;
    }
}
```