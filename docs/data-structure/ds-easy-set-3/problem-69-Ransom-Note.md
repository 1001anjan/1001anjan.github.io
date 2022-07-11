---
layout: default
title:  Ransom Note
parent: Data Structure Easy Set 3
grand_parent: Data Structure
nav_order: 6
permalink: /problem-69-Ransom-Note/
---
# Ransom Note

Given two strings ransomNote and magazine, return true if ransomNote can be constructed by using the letters from magazine and false otherwise.

Each letter in magazine can only be used once in ransomNote.

##### Example 1:
```markdown
Input: ransomNote = "a", magazine = "b"
Output: false
```
##### Example 2:
```markdown
Input: ransomNote = "aa", magazine = "ab"
Output: false
```
##### Example 3:
```markdown
Input: ransomNote = "aa", magazine = "aab"
Output: true
```
##### Constraints:
* 1 <= ransomNote.length, magazine.length <= 105
* ransomNote and magazine consist of lowercase English letters.

### Solution
```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        if(ransomNote.length()>magazine.length()) return false;
        
        Map<Character,Integer> m1 = new HashMap<Character, Integer>();
        Map<Character,Integer> m2 = new HashMap<Character, Integer>();
        
        for(int i = 0; i <ransomNote.length(); i++){
            if(m1.containsKey(ransomNote.charAt(i))){
                m1.put(ransomNote.charAt(i),(int)m1.get(ransomNote.charAt(i))+1);
            }else{
                m1.put(ransomNote.charAt(i),1);
            }
        }
        
        for(int i = 0; i <magazine.length(); i++){
            if(m2.containsKey(magazine.charAt(i))){
                m2.put(magazine.charAt(i),(int)m2.get(magazine.charAt(i))+1);
            }else{
                m2.put(magazine.charAt(i),1);
            }
        }
        
        for(Map.Entry<Character,Integer> e : m1.entrySet()){
            if(!m2.containsKey(e.getKey())) return false;
            else
                if((int)e.getValue() > (int)m2.get(e.getKey())) return false;
        }
        return true;
    }
}
```
##### Faster Solution
```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        int[] count=new int[26];
        for(int i=0;i<magazine.length();i++){
            char ch=magazine.charAt(i);
            count[ch-'a']++;
        }
        for(int i=0;i<ransomNote.length();i++){
            char ch=ransomNote.charAt(i);
            if(--count[ch-'a']<0){
                return false;
            }    
        }
        return true;
    }
}
```