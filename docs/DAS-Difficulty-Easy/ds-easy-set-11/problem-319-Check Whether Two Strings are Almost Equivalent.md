---
layout: default
title: Check Whether Two Strings are Almost Equivalent
parent: Easy Set 11
grand_parent: DSA Easy Difficulty
nav_order: 9
permalink: /problem-319-Check Whether Two Strings are Almost Equivalent/
---
# Check Whether Two Strings are Almost Equivalent

Two strings word1 and word2 are considered almost equivalent if the differences between the frequencies of each letter from 'a' to 'z' between word1 and word2 is at most 3.

Given two strings word1 and word2, each of length n, return true if word1 and word2 are almost equivalent, or false otherwise.

The frequency of a letter x is the number of times it occurs in the string.

##### Example 1:
```markdown
Input: word1 = "aaaa", word2 = "bccb"
Output: false
Explanation: There are 4 'a's in "aaaa" but 0 'a's in "bccb".
The difference is 4, which is more than the allowed 3.
```
##### Example 2:
```markdown
Input: word1 = "abcdeef", word2 = "abaaacc"
Output: true
Explanation: The differences between the frequencies of each letter in word1 and word2 are at most 3:
- 'a' appears 1 time in word1 and 4 times in word2. The difference is 3.
- 'b' appears 1 time in word1 and 1 time in word2. The difference is 0.
- 'c' appears 1 time in word1 and 2 times in word2. The difference is 1.
- 'd' appears 1 time in word1 and 0 times in word2. The difference is 1.
- 'e' appears 2 times in word1 and 0 times in word2. The difference is 2.
- 'f' appears 1 time in word1 and 0 times in word2. The difference is 1.
```
##### Example 3:
```markdown
Input: word1 = "cccddabba", word2 = "babababab"
Output: true
Explanation: The differences between the frequencies of each letter in word1 and word2 are at most 3:
- 'a' appears 2 times in word1 and 4 times in word2. The difference is 2.
- 'b' appears 2 times in word1 and 5 times in word2. The difference is 3.
- 'c' appears 3 times in word1 and 0 times in word2. The difference is 3.
- 'd' appears 2 times in word1 and 0 times in word2. The difference is 2.
```
##### Constraints:
* n == word1.length == word2.length
* 1 <= n <= 100
* word1 and word2 consist only of lowercase English letters.

### Solution:
```java
class Solution {
    public boolean checkAlmostEquivalent(String word1, String word2) {
        int[] dp1 = getFrequency(word1);
        int[] dp2 = getFrequency(word2);
        
        for(int i = 0; i < 26; i++){
            if(Math.abs(dp1[i] - dp2[i]) > 3) return false;
        }
        return true;
    }
    
    public int[] getFrequency(String str){
        int[] dp = new int[26];
        for(char c : str.toCharArray()) dp[c - 'a']++;
        return dp;
    }
}
```