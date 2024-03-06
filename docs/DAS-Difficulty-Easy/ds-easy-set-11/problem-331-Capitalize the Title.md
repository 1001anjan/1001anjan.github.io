---
layout: default
title: Capitalize the Title
parent: Easy Set 11
grand_parent: DSA Easy
nav_order: 21
permalink: /problem-331-Capitalize the Title/
---
# Capitalize the Title
You are given a string title consisting of one or more words separated by a single space, where each word consists of English letters. Capitalize the string by changing the capitalization of each word such that:

* If the length of the word is 1 or 2 letters, change all letters to lowercase.
* Otherwise, change the first letter to uppercase and the remaining letters to lowercase.
Return the capitalized title.

##### Example 1:
```markdown
Input: title = "capiTalIze tHe titLe"
Output: "Capitalize The Title"
Explanation:
Since all the words have a length of at least 3, the first letter of each word is uppercase, and the remaining letters are lowercase.
```
##### Example 2:
```markdown
Input: title = "First leTTeR of EACH Word"
Output: "First Letter of Each Word"
Explanation:
The word "of" has length 2, so it is all lowercase.
The remaining words have a length of at least 3, so the first letter of each remaining word is uppercase, and the remaining letters are lowercase.
```
##### Example 3:
```markdown
Input: title = "i lOve leetcode"
Output: "i Love Leetcode"
Explanation:
The word "i" has length 1, so it is lowercase.
The remaining words have a length of at least 3, so the first letter of each remaining word is uppercase, and the remaining letters are lowercase.
```
##### Constraints:
* 1 <= title.length <= 100
* title consists of words separated by a single space without any leading or trailing spaces.
* Each word consists of uppercase and lowercase English letters and is non-empty.

### Solution:
```java
class Solution {
    public String capitalizeTitle(String title) {
        StringBuilder sb = new StringBuilder();
        String[] words = title.split(" ");
        for(String str : words){
            str = str.toLowerCase();
            if(str.length() <= 2){
                sb.append(str).append(" ");
            }else{
                sb.append(Character.toUpperCase(str.charAt(0)))
                    .append(str.substring(1,str.length())).append(" ");
            }
        }
        return sb.substring(0,sb.length() - 1).toString();
    }
}
```