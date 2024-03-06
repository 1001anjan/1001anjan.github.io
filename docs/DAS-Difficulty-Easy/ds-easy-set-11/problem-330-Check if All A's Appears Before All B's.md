---
layout: default
title: Check if All A's Appears Before All B's
parent: Easy Set 11
grand_parent: DSA Easy
nav_order: 20
permalink: /problem-330-Check if All A's Appears Before All B's/
---
# Check if All A's Appears Before All B's

Given a string s consisting of only the characters 'a' and 'b', return true if every 'a' appears before every 'b' in the string. Otherwise, return false.

##### Example 1:
```markdown
Input: s = "aaabbb"
Output: true
Explanation:
The 'a's are at indices 0, 1, and 2, while the 'b's are at indices 3, 4, and 5.
Hence, every 'a' appears before every 'b' and we return true.
```
##### Example 2:
```markdown
Input: s = "abab"
Output: false
Explanation:
There is an 'a' at index 2 and a 'b' at index 1.
Hence, not every 'a' appears before every 'b' and we return false.
```
##### Example 3:
```markdown
Input: s = "bbb"
Output: true
Explanation:
There are no 'a's, hence, every 'a' appears before every 'b' and we return true.
```
##### Constraints:
* 1 <= s.length <= 100
* s[i] is either 'a' or 'b'.

### Solution:
```java
class Solution {
    public boolean checkString(String s) {
        // traversing all a's first
        int i = 0;
        int n = s.length();
        while(i < n && s.charAt(i) == 'a') i++;
        if(i == n) return true;
         while(i < n &&s.charAt(i) == 'b') i++;
        return i == n;
    }
}
```