---
layout: default
title: Rearrange Spaces Between Words
parent: Data Structure Easy Set 8
grand_parent: Data Structure
nav_order: 21
permalink: /problem-241-Rearrange-Spaces-Between-Words/
---
# Rearrange Spaces Between Words

You are given a string text of words that are placed among some number of spaces. Each word consists of one or more lowercase English letters and are separated by at least one space. It's guaranteed that text contains at least one word.

Rearrange the spaces so that there is an equal number of spaces between every pair of adjacent words and that number is maximized. If you cannot redistribute all the spaces equally, place the extra spaces at the end, meaning the returned string should be the same length as text.

Return the string after rearranging the spaces.

##### Example 1:
```markdown
Input: text = "  this   is  a sentence "
Output: "this   is   a   sentence"
Explanation: There are a total of 9 spaces and 4 words. We can evenly divide the 9 spaces between the words: 9 / (4-1) = 3 spaces.
```
##### Example 2:
```markdown
Input: text = " practice   makes   perfect"
Output: "practice   makes   perfect "
Explanation: There are a total of 7 spaces and 3 words. 7 / (3-1) = 3 spaces plus 1 extra space. We place this extra space at the end of the string.
```
##### Constraints:
* 1 <= text.length <= 100
* text consists of lowercase English letters and ' '.
* text contains at least one word.

### Solution:
```java
class Solution {
    public String reorderSpaces(String text) {
        int totalLen = text.length();
        if(totalLen == 1) return text;
        String[] words = text.trim().split("\\s+");
        int len = 0;
        for(String s : words) len += s.length();
        
        int space =  totalLen - len;
        
        boolean isOne = false;
        int extra = 0;
        if(words.length == 1){
            isOne = true;
        }else{
            extra = space - (space / (words.length - 1))*(words.length - 1);
            space = space / (words.length - 1);
        }

        StringBuilder sb = new StringBuilder();
        for(String s : words){
            sb.append(s);
            for(int i = 1; i <= space; i++) sb.append(" ");
        }
        
        if(!isOne){
            sb.setLength(sb.length() - space);
        }
        for(int i = 1; i <= extra; i++) sb.append(" ");

        return sb.toString();
    }
}
```