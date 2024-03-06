---
layout: default
title:  Reverse Vowels of a String
parent: Easy Set 3
grand_parent: DSA Easy
nav_order: 1
permalink: /problem-64-Reverse-Vowels-of-a-String/
---
#   Reverse Vowels of a String
Given a string s, reverse only all the vowels in the string and return it.

The vowels are 'a', 'e', 'i', 'o', and 'u', and they can appear in both cases.

##### Example 1:
```markdown
Input: s = "hello"
Output: "holle"
```
##### Example 2:
```markdown
Input: s = "leetcode"
Output: "leotcede"
```
##### Constraints:
* 1 <= s.length <= 3 * 105
* s consist of printable ASCII characters.

### Solution
```java
class Solution {
    public String reverseVowels(String s) {
        char[] str = new char[s.length()];
        str = s.toCharArray();
        int i = 0;
        int j = s.length() - 1;
        char ch;
        while(i<j){
            while(i<j && !isVowel(str[i])) i++;
            while(i<j && !isVowel(str[j])) j--;
            if(i<j){
               ch = str[i];
                str[i] = str[j];
                str[j] = ch;
                i++;
                j--;
            }
        }
        return String.valueOf(str);
    }
    
    public boolean isVowel(char ch){
        if(ch == 'A' || ch =='a' || ch == 'e' || ch == 'E' || ch == 'I' ||
           ch =='i' || ch == 'O' || ch == 'o' || ch == 'u' || ch == 'U') return true;
        return false;
    }
}
```