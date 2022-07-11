---
layout: default
title: Detect Capital
parent: Data Structure Easy Set 3
grand_parent: Data Structure
nav_order: 32
permalink: /problem-95-Detect-Capital/
---
# Detect Capital

We define the usage of capitals in a word to be right when one of the following cases holds:

* All letters in this word are capitals, like "USA".
* All letters in this word are not capitals, like "leetcode".
* Only the first letter in this word is capital, like "Google".
* Given a string word, return true if the usage of capitals in it is right.

##### Example 1:
```markdown
Input: word = "USA"
Output: true
```
##### Example 2:
```markdown
Input: word = "FlaG"
Output: false
```
##### Constraints:
* 1 <= word.length <= 100
* word consists of lowercase and uppercase English letters.

##### Solution:
```java
class Solution {
    public boolean detectCapitalUse(String word) {
        if(Character.isUpperCase(word.charAt(0))){
            String s1 = word.toUpperCase();
            if(word.equals(s1)) return true;
            s1 = word.charAt(0) + word.substring(1,word.length()).toLowerCase();
            if(word.equals(s1)) return true;
            return false;
        }else{
            String s1 = word.toLowerCase();
            if(word.equals(s1)) return true;
            return false;
        }
    }
}
```
```java
class Solution {
    public boolean detectCapitalUse(String word) {
        return word.matches("[A-Z]*|.[a-z]*");
    }
}
```
#### Faster 
```java
class Solution {
    public boolean detectCapitalUse(String word) {
        int n = word.length();
        if (n == 1) {
            return true;
        }

        // case 1: All capital
        if (Character.isUpperCase(word.charAt(0)) && Character.isUpperCase(word.charAt(1))) {
            for (int i = 2; i < n; i++) {
                if (Character.isLowerCase(word.charAt(i))) {
                    return false;
                }
            }
        // case 2 and case 3
        } else {
            for (int i = 1; i < n; i++) {
                if (Character.isUpperCase(word.charAt(i))) {
                    return false;
                }
            }
        }

        // if pass one of the cases
        return true;
    }
}
```