---
layout: default
title: Divide a String Into Groups of Size k
parent: Easy Set 11
grand_parent: DSA Easy Difficulty
nav_order: 23
permalink: /problem-333-Divide a String Into Groups of Size k/
---
# Divide a String Into Groups of Size k

A string s can be partitioned into groups of size k using the following procedure:

* The first group consists of the first k characters of the string, the second group consists of the next k characters of the string, and so on. Each character can be a part of exactly one group.
* For the last group, if the string does not have k characters remaining, a character fill is used to complete the group.

Note that the partition is done so that after removing the fill character from the last group (if it exists) and concatenating all the groups in order, the resultant string should be s.

Given the string s, the size of each group k and the character fill, return a string array denoting the composition of every group s has been divided into, using the above procedure.

##### Example 1:
```markdown
Input: s = "abcdefghi", k = 3, fill = "x"
Output: ["abc","def","ghi"]
Explanation:
The first 3 characters "abc" form the first group.
The next 3 characters "def" form the second group.
The last 3 characters "ghi" form the third group.
Since all groups can be completely filled by characters from the string, we do not need to use fill.
Thus, the groups formed are "abc", "def", and "ghi".
```
##### Example 2:
```markdown
Input: s = "abcdefghij", k = 3, fill = "x"
Output: ["abc","def","ghi","jxx"]
Explanation:
Similar to the previous example, we are forming the first three groups "abc", "def", and "ghi".
For the last group, we can only use the character 'j' from the string. To complete this group, we add 'x' twice.
Thus, the 4 groups formed are "abc", "def", "ghi", and "jxx".
```
##### Constraints:
* 1 <= s.length <= 100
* s consists of lowercase English letters only.
* 1 <= k <= 100
* fill is a lowercase English letter.

### Solution:
```java
class Solution {
    public String[] divideString(String s, int k, char fill) {
        int n = s.length();
        String[] ans = new String[(int)Math.ceil((double)n/k)];
        StringBuilder sb = new StringBuilder();
        int i = 0;
        int l = 0;
        while(i < n){
            sb.setLength(0);
            int m = k;
            while(m > 0 && i < n){
                sb.append(s.charAt(i));
                i++;
                m--;
            }
            while(m > 0){
                sb.append(fill);
                m--;
            }
            ans[l++] = sb.toString();
        }
        
        return ans;
    }
}
```