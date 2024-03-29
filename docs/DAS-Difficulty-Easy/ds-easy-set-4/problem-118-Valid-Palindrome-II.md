---
layout: default
title: Valid Palindrome II
parent: Easy Set 4
grand_parent: DSA Easy
nav_order: 18
permalink: /problem-118-Valid-Palindrome-II/
---
# Valid Palindrome II
Given a string s, return true if the s can be palindrome after deleting at most one character from it.

##### Example 1:
```markdown
Input: s = "aba"
Output: true
```
##### Example 2:
```markdown
Input: s = "abca"
Output: true
Explanation: You could delete the character 'c'.
```
##### Example 3:
```markdown
Input: s = "abc"
Output: false
```
##### Constraints:
* 1 <= s.length <= 105
* s consists of lowercase English letters.

### Solution:
```java
class Solution {
    private boolean checkPalindrome(String s, int i, int j) {
        while (i < j) {
            if (s.charAt(i) != s.charAt(j)) {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }
    
    public boolean validPalindrome(String s) {
        int i = 0;
        int j = s.length() - 1;
        
        while (i < j) {
            // Found a mismatched pair - try both deletions
            if (s.charAt(i) != s.charAt(j)) {
                return (checkPalindrome(s, i, j - 1) || checkPalindrome(s, i + 1, j));
            } 
            i++;
            j--;
        }
        
        return true;
    }
}
```