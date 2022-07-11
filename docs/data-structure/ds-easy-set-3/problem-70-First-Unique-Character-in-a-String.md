---
layout: default
title: First Unique Character in a String
parent: Data Structure Easy Set 3
grand_parent: Data Structure
nav_order: 7
permalink: /problem-70-First-Unique-Character-in-a-String/
---
# First Unique Character in a String
Given a string s, find the first non-repeating character in it and return its index. If it does not exist, return -1.

##### Example 1:
```markdown
Input: s = "leetcode"
Output: 0
```
##### Example 2:
```markdown
Input: s = "loveleetcode"
Output: 2
```
##### Example 3:
```markdown
Input: s = "aabb"
Output: -1
```
##### Constraints:
* 1 <= s.length <= 105
* s consists of only lowercase English letters.

### Solution
```java
class Solution {
    public int firstUniqChar(String s) {
       Map<Character,Integer> m = new HashMap<Character,Integer>();
        for(int i=0; i<s.length(); i++){
            if(m.containsKey(s.charAt(i)))
                m.put(s.charAt(i),(int)m.get(s.charAt(i))+1);
            else
                m.put(s.charAt(i),1);
        }
        for(int i=0; i<s.length(); i++){
            if((int)m.get(s.charAt(i)) == 1) return i;
        }
        return -1;
    }
}
```
###### Without hashMap
```java
class Solution {
    public int firstUniqChar(String s) {
        int[] count = new int[26];
        int n = s.length();
        // build char count bucket : <charIndex, count>
        for (int i = 0; i < n; i++) {            
            int index = s.charAt(i) - 'a';
            count[index]++;
        }
        
        // find the index
        for (int i = 0; i < n; i++) {
            int index = s.charAt(i) - 'a';
            if (count[index] == 1) {
                return i;
            }
                
        }
        return -1;
    }
}
```