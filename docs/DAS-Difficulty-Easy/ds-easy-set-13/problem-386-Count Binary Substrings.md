---
layout: default
title: Count Binary Substrings
parent: Easy Set 13
grand_parent: DSA Easy
nav_order: 16
permalink: /problem-386-Count Binary Substrings/
---
# Count Binary Substrings
Given a binary string s, return the number of non-empty substrings that have the same number of 0's and 1's, and all the 0's and all the 1's in these substrings are grouped consecutively.

Substrings that occur multiple times are counted the number of times they occur.

##### Example 1:
```markdown
Input: s = "00110011"
Output: 6
Explanation: There are 6 substrings that have equal number of consecutive 1's and 0's: "0011", "01", "1100", "10", "0011", and "01".
Notice that some of these substrings repeat and are counted the number of times they occur.
Also, "00110011" is not a valid substring because all the 0's (and 1's) are not grouped together.
```
##### Example 2:
```markdown
Input: s = "10101"
Output: 4
Explanation: There are 4 substrings: "10", "01", "10", "01" that have equal number of consecutive 1's and 0's.
```
##### Constraints:
* 1 <= s.length <= 105
* s[i] is either '0' or '1'.

### Solution:
```java
class Solution {
    public int countBinarySubstrings(String s) {
        int count = 0, curr = 1, prev = 0;
        char[] str = s.toCharArray();
        for(int i = 1; i < str.length; i++){
            if(str[i - 1] != str[i]){
                count += Math.min(curr,prev);
                prev = curr;
                curr = 1;
            }else{
                curr++;
            }
        }
        count += Math.min(curr,prev);
        return count;
    }
}
```