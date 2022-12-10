---
layout: default
title: Isomorphic Strings
parent: Data Structure Easy Set 13
grand_parent: Data Structure
nav_order: 7
permalink: /problem-377-Isomorphic Strings/
---
# Isomorphic Strings
Given two strings s and t, determine if they are isomorphic.

Two strings s and t are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

##### Example 1:
```markdown
Input: s = "egg", t = "add"
Output: true
```
##### Example 2:
```markdown
Input: s = "foo", t = "bar"
Output: false
```
##### Example 3:
```markdown
Input: s = "paper", t = "title"
Output: true
```
##### Constraints:
* 1 <= s.length <= 5 * 104
* t.length == s.length
* s and t consist of any valid ascii character.

### Solution:
```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        Map<Character,Character> mp1 = new HashMap<>();
        Map<Character,Character> mp2 = new HashMap<>();
        
        for(int i = 0; i < s.length(); i++){
            char ch1 = s.charAt(i);
            char ch2 = t.charAt(i);
            boolean s1 = mp1.containsKey(ch1);
            boolean s2 = mp2.containsKey(ch2);
            
            if(s1 != s2) return false;
                
            if(!s1){
                mp1.put(ch1,ch2);
                mp2.put(ch2,ch1);
            }else{
                if(mp1.get(ch1) != ch2 || mp2.get(ch2) != ch1) return false;
            }
        }
        return true;
    }
}
```

##### Improvement 
```markdown
class Solution {
    public boolean isIsomorphic(String s, String t) {
        
        int[] mappingDictStoT = new int[256];
        Arrays.fill(mappingDictStoT, -1);
        
        int[] mappingDictTtoS = new int[256];
        Arrays.fill(mappingDictTtoS, -1);
        
        for (int i = 0; i < s.length(); ++i) {
            char c1 = s.charAt(i);
            char c2 = t.charAt(i);
            
            // Case 1: No mapping exists in either of the dictionaries
            if (mappingDictStoT[c1] == -1 && mappingDictTtoS[c2] == -1) {
                mappingDictStoT[c1] = c2;
                mappingDictTtoS[c2] = c1;
            }
            
            // Case 2: Ether mapping doesn't exist in one of the dictionaries or Mapping exists and
            // it doesn't match in either of the dictionaries or both 
            else if (!(mappingDictStoT[c1] == c2 && mappingDictTtoS[c2] == c1)) {
                return false;
            }
        }
        
        return true;
    }
}
```