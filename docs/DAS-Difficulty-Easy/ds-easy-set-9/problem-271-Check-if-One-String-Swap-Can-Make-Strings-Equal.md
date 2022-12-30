---
layout: default
title: Check if Binary String Has at Most One Segment of Ones
parent: Easy Set 9
grand_parent: DSA Easy Difficulty
nav_order: 21
permalink: /problem-271-Check-if-One-String-Swap-Can-Make-Strings-Equal/
---
# Check if One String Swap Can Make Strings Equal
You are given two strings s1 and s2 of equal length. A string swap is an operation where you choose two indices in a string (not necessarily different) and swap the characters at these indices.

Return true if it is possible to make both strings equal by performing at most one string swap on exactly one of the strings. Otherwise, return false.

##### Example 1:
```markdown
Input: s1 = "bank", s2 = "kanb"
Output: true
Explanation: For example, swap the first character with the last character of s2 to make "bank".
```
##### Example 2:
```markdown
Input: s1 = "attack", s2 = "defend"
Output: false
Explanation: It is impossible to make them equal with one string swap.
```
##### Example 3:
```markdown
Input: s1 = "kelb", s2 = "kelb"
Output: true
Explanation: The two strings are already equal, so no string swap operation is required.
```
##### Constraints:
* 1 <= s1.length, s2.length <= 100
* s1.length == s2.length
* s1 and s2 consist of only lowercase English letters.

### Solution:
```java
class Solution {
    public boolean areAlmostEqual(String s1, String s2) {
        List<Integer> indexs = new ArrayList<>();
        for(int i = 0; i < s1.length(); i++){
            if(s1.charAt(i) != s2.charAt(i)){
                indexs.add(i);
            }
            if(indexs.size() > 2) return false;
        }
        if(indexs.size() == 0) return true;
        if(indexs.size() == 1) return false;
        return s1.charAt(indexs.get(0)) == s2.charAt(indexs.get(1)) &&
            s1.charAt(indexs.get(1)) == s2.charAt(indexs.get(0));
    }
}
```
####### Another way
```java
class Solution {
    public boolean areAlmostEqual(String s1, String s2) {
        if(s1.equals(s2)) return true;
        List<Integer> indexs = new ArrayList<>();
        for(int i = 0; i < s1.length(); i++){
            if(s1.charAt(i) != s2.charAt(i)){
                indexs.add(i);
            }
            if(indexs.size() > 2) return false;
        }
        if(indexs.size() == 2){
            return s1.charAt(indexs.get(0)) == s2.charAt(indexs.get(1)) &&
                s1.charAt(indexs.get(1)) == s2.charAt(indexs.get(0));
        } 
        
        return false;
    }
}
```