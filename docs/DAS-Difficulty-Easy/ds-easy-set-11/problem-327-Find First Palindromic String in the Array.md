---
layout: default
title: Find First Palindromic String in the Array
parent: Easy Set 11
grand_parent: DSA Easy
nav_order: 17
permalink: /problem-327-Find First Palindromic String in the Array/
---
# Find First Palindromic String in the Array
Given an array of strings words, return the first palindromic string in the array. If there is no such string, return an empty string "".

A string is palindromic if it reads the same forward and backward.

##### Example 1:
```markdown
Input: words = ["abc","car","ada","racecar","cool"]
Output: "ada"
Explanation: The first string that is palindromic is "ada".
Note that "racecar" is also palindromic, but it is not the first.
```
##### Example 2:
```markdown
Input: words = ["notapalindrome","racecar"]
Output: "racecar"
Explanation: The first and only string that is palindromic is "racecar".
```
##### Example 3:
```markdown
Input: words = ["def","ghi"]
Output: ""
Explanation: There are no palindromic strings, so the empty string is returned.
```
##### Constraints:
* 1 <= words.length <= 100
* 1 <= words[i].length <= 100
* words[i] consists only of lowercase English letters.

### Solution:
```java
class Solution {
    public String firstPalindrome(String[] words) {
        for(String str : words){
            if(checkPalindrome(str)) return str;
        }
        return "";
    }
    
    public boolean checkPalindrome(String str){
        int i = 0;
        int j = str.length() - 1;
        while(i < j){
            if(str.charAt(i) != str.charAt(j)) return false;
            i++;
            j--;
        }
        return true;
    }
}
```