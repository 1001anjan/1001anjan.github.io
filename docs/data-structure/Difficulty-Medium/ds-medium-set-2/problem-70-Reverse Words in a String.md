---
layout: default
title: Reverse Words in a String
parent: Data Structure Medium Set 2
grand_parent: Data Structure
nav_order: 20
permalink: /problem-70-Reverse Words in a String/
---
# Reverse Words in a String
Given an input string s, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

Note that s may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

##### Example 1:
```markdown
Input: s = "the sky is blue"
Output: "blue is sky the"
```
##### Example 2:
```markdown
Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```
##### Example 3:
```markdown
Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```
##### Constraints:
* 1 <= s.length <= 10^4
* s contains English letters (upper-case and lower-case), digits, and spaces ' '.
* There is at least one word in s.

Follow-up: If the string data type is mutable in your language, can you solve it in-place with O(1) extra space?

### Solution:
```java
class Solution {
    public String reverseWords(String s) {
        String[] strs = s.trim().split("\\s+");
        StringBuilder sb = new StringBuilder();
        for(int i = strs.length - 1; i >= 0; i--){
            sb.append(strs[i]).append(" ");
        }
        return sb.substring(0, sb.length() - 1).toString();
    }
}
```