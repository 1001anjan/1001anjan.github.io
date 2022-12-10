---
layout: default
title: Remove All Adjacent Duplicates In String
parent: Data Structure Easy Set 6
grand_parent: Data Structure
nav_order: 9
permalink: /problem-169-Remove-All-Adjacent-Duplicates-In-String/
---
# Remove All Adjacent Duplicates In String

You are given a string s consisting of lowercase English letters. A duplicate removal consists of choosing two adjacent and equal letters and removing them.

We repeatedly make duplicate removals on s until we no longer can.

Return the final string after all such duplicate removals have been made. It can be proven that the answer is unique.

##### Example 1:
```markdown
Input: s = "abbaca"
Output: "ca"
Explanation:
For example, in "abbaca" we could remove "bb" since the letters are adjacent and equal, and this is the only possible move.  The result of this move is that the string is "aaca", of which only "aa" is possible, so the final string is "ca".
```
##### Example 2:
```markdown
Input: s = "azxxzy"
Output: "ay"
```
##### Constraints:
* 1 <= s.length <= 105
* s consists of lowercase English letters.

### Solution:
```markdown
class Solution {
    public String removeDuplicates(String s) {
        StringBuilder sb = new StringBuilder();
        sb.append(s.charAt(0));
        for(int i=1; i<s.length(); i++){
            if(sb.length()>0 && sb.charAt(sb.length()-1) == s.charAt(i)){
               // sb.delete(sb.length()-1, sb.length());
                sb.deleteCharAt(sb.length()-1);
            }else{
                sb.append(s.charAt(i));
            }
        }
        return sb.toString();
    }
}
```

