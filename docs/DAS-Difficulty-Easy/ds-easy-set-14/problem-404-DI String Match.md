---
layout: default
title: DI String Match
parent: Easy Set 14
grand_parent: DSA Easy Difficulty
nav_order: 4
permalink: /problem-404-DI String Match/
---
# DI String Match
A permutation perm of n + 1 integers of all the integers in the range [0, n] can be represented as a string s of length n where:

* s[i] == 'I' if perm[i] < perm[i + 1], and
* s[i] == 'D' if perm[i] > perm[i + 1].
Given a string s, reconstruct the permutation perm and return it. If there are multiple valid permutations perm, return any of them.

##### Example 1:
```markdown
Input: s = "IDID"
Output: [0,4,1,3,2]
```
##### Example 2:
```markdown
Input: s = "III"
Output: [0,1,2,3]
```
##### Example 3:
```markdown
Input: s = "DDI"
Output: [3,2,0,1]
```
##### Constraints:
* 1 <= s.length <= 105
* s[i] is either 'I' or 'D'.

### Solution:
```java
class Solution {
    public int[] diStringMatch(String s) {
        char[] chs = s.toCharArray();
        int[] ans = new int[chs.length + 1];
        int u = chs.length;
        int l = 0;
        for(int i = 0; i < chs.length; i++){
            if(chs[i] == 'I'){
                ans[i] = l++;
            }else{
                ans[i] = u--;
            }
        }
        ans[chs.length] = l;
        return ans;
    }
}
```