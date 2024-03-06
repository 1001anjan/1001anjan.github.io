---
layout: default
title: Delete Characters to Make Fancy String
parent: Easy Set 10
grand_parent: DSA Easy
nav_order: 21
permalink: /problem-301-Delete Characters to Make Fancy String/
---
# Delete Characters to Make Fancy String

A fancy string is a string where no three consecutive characters are equal.

Given a string s, delete the minimum possible number of characters from s to make it fancy.

Return the final string after the deletion. It can be shown that the answer will always be unique.

##### Example 1:
```markdown
Input: s = "leeetcode"
Output: "leetcode"
Explanation:
Remove an 'e' from the first group of 'e's to create "leetcode".
No three consecutive characters are equal, so return "leetcode".
```
##### Example 2:
```markdown
Input: s = "aaabaaaa"
Output: "aabaa"
Explanation:
Remove an 'a' from the first group of 'a's to create "aabaaaa".
Remove two 'a's from the second group of 'a's to create "aabaa".
No three consecutive characters are equal, so return "aabaa".
```
##### Example 3:
```markdown
Input: s = "aab"
Output: "aab"
Explanation: No three consecutive characters are equal, so return "aab".
```
##### Constraints:
* 1 <= s.length <= 10^5
* s consists only of lowercase English letters.

### Solution:
```java
class Solution {
    public String makeFancyString(String s) {
        StringBuilder sb = new StringBuilder();
        char[] chr = s.toCharArray();
        sb.append(chr[0]);
        int c = 1;
        for(int i = 1; i < chr.length; i++){
            if(chr[i - 1] == chr[i]){
                c++;
                if(c < 3){
                    sb.append(chr[i]);
                }
            }else{
                c = 1;
                sb.append(chr[i]);
            } 
        }
        return sb.toString(); 
    }
}
```