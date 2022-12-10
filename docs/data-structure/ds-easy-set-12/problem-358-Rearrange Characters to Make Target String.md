---
layout: default
title: Rearrange Characters to Make Target String
parent: Data Structure Easy Set 12
grand_parent: Data Structure
nav_order: 18
permalink: /problem-358-Rearrange Characters to Make Target String/
---
# Rearrange Characters to Make Target String
You are given two 0-indexed strings s and target. You can take some letters from s and rearrange them to form new strings.

Return the maximum number of copies of target that can be formed by taking letters from s and rearranging them.

##### Example 1:
```markdown
Input: s = "ilovecodingonleetcode", target = "code"
Output: 2
Explanation:
For the first copy of "code", take the letters at indices 4, 5, 6, and 7.
For the second copy of "code", take the letters at indices 17, 18, 19, and 20.
The strings that are formed are "ecod" and "code" which can both be rearranged into "code".
We can make at most two copies of "code", so we return 2.
```
##### Example 2:
```markdown
Input: s = "abcba", target = "abc"
Output: 1
Explanation:
We can make one copy of "abc" by taking the letters at indices 0, 1, and 2.
We can make at most one copy of "abc", so we return 1.
Note that while there is an extra 'a' and 'b' at indices 3 and 4, we cannot reuse the letter 'c' at index 2, so we cannot make a second copy of "abc".
```
##### Example 3:
```markdown
Input: s = "abbaccaddaeea", target = "aaaaa"
Output: 1
Explanation:
We can make one copy of "aaaaa" by taking the letters at indices 0, 3, 6, 9, and 12.
We can make at most one copy of "aaaaa", so we return 1.
```
##### Constraints:
* 1 <= s.length <= 100
* 1 <= target.length <= 10
* s and target consist of lowercase English letters.

### Solution:
```java
class Solution {
    public int rearrangeCharacters(String s, String target) {
        int[] dp1 = new int[26];
        int[] dp2 = new int[26];
        for(char ch : s.toCharArray()) dp1[ch - 'a']++;
        for(char ch : target.toCharArray()) dp2[ch - 'a']++;
        int max = Integer.MAX_VALUE;
        for(int i = 0; i < 26; i++){
            if(dp2[i] != 0)
                max= Math.min(max,dp1[i] / dp2[i]);
        }
        
        return max;
    }
}
```