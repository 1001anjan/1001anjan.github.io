---
layout: default
title: Maximum Product of Word Lengths
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 28
permalink: /problem-128-Maximum Product of Word Lengths/
---
# Maximum Product of Word Lengths
Given a string array words, return the maximum value of length(word[i]) * length(word[j]) where the two words do not share common letters. If no such two words exist, return 0.

##### Example 1:
```markdown
Input: words = ["abcw","baz","foo","bar","xtfn","abcdef"]
Output: 16
Explanation: The two words can be "abcw", "xtfn".
```
##### Example 2:
```markdown
Input: words = ["a","ab","abc","d","cd","bcd","abcd"]
Output: 4
Explanation: The two words can be "ab", "cd".
```
##### Example 3:
```markdown
Input: words = ["a","aa","aaa","aaaa"]
Output: 0
Explanation: No such pair of words.
```
##### Constraints:
* 2 <= words.length <= 1000
* 1 <= words[i].length <= 1000
* words[i] consists only of lowercase English letters.

### Solution:
```java
class Solution {
    public int maxProduct(String[] words) {
        // base condition
        if(words == null || words.length < 2) return 0;

        int maxProd = 0;
        int[] value = new int [words.length];

        for(int i = 0;  i < words.length; i++){
            for(int j = 0; j < words[i].length(); j++){
                value[i] |= 1 << (words[i].charAt(j) - 'a');
            }
        }

        for(int i = 0; i < words.length - 1; i++){
            for(int j = i + 1; j < words.length; j++){
                if((value[i] & value[j]) == 0){
                    maxProd = Math.max(maxProd, words[i].length() * words[j].length());
                }
            }
        }

        return maxProd;
    }
}
```