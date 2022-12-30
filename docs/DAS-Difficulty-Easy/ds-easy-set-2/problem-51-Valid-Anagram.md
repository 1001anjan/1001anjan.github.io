---
layout: default
title: Valid Anagram
parent: Easy Set 2
grand_parent: DSA Easy Difficulty
nav_order: 20
permalink: /problem-51-Valid-Anagram/
---
# Valid Anagram

Given two strings s and t, return true if t is an anagram of s, and false otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

##### Example 1:
```markdown
Input: s = "anagram", t = "nagaram"
Output: true
```
##### Example 2:
```markdown
Input: s = "rat", t = "car"
Output: false
```
##### Constraints:
* 1 <= s.length, t.length <= 5 * 104
* s and t consist of lowercase English letters.

### Solution
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length() != t.length()) return false;
        Map<Character, Integer> map1 = new HashMap<Character, Integer>();
        Map<Character, Integer> map2 = new HashMap<Character, Integer>();
        for(int i=0; i<s.length(); i++){
            if(map1.containsKey(s.charAt(i))){
                map1.put(s.charAt(i), map1.get(s.charAt(i))+1);
            }else{
                map1.put(s.charAt(i), 1);
            }
            if(map2.containsKey(t.charAt(i))){
                map2.put(t.charAt(i), map2.get(t.charAt(i))+1);
            }else{
                map2.put(t.charAt(i), 1);
            }
        }
        for(Character ch : map1.keySet()){
          if(!map2.containsKey(ch)) return false;
          if((int)map1.get(ch) != (int)map2.get(ch)) return false;  
        }
        return true;
    }
}
```

##### try using simple map or only using array
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        int[] arr = new int[26];
        if(s.length() != t.length()) 
            return false;
        
        for(char a: s.toCharArray())
            arr[a - 'a']++;
        
        for(char b : t.toCharArray())
            arr[b - 'a']--;
        
        for(int i : arr){
            if(i > 0)
                return false;
        }
     return true;
    }
}
```