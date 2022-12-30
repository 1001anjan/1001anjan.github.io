---
layout: default
title: Verifying an Alien Dictionary
parent: Easy Set 14
grand_parent: DSA Easy Difficulty
nav_order: 5
permalink: /problem-405-Verifying an Alien Dictionary/
---
# Verifying an Alien Dictionary
In an alien language, surprisingly, they also use English lowercase letters, but possibly in a different order. The order of the alphabet is some permutation of lowercase letters.

Given a sequence of words written in the alien language, and the order of the alphabet, return true if and only if the given words are sorted lexicographically in this alien language.

##### Example 1:
```markdown
Input: words = ["hello","leetcode"], order = "hlabcdefgijkmnopqrstuvwxyz"
Output: true
Explanation: As 'h' comes before 'l' in this language, then the sequence is sorted.
```
##### Example 2:
```markdown
Input: words = ["word","world","row"], order = "worldabcefghijkmnpqstuvxyz"
Output: false
Explanation: As 'd' comes after 'l' in this language, then words[0] > words[1], hence the sequence is unsorted.
```
##### Example 3:
```markdown
Input: words = ["apple","app"], order = "abcdefghijklmnopqrstuvwxyz"
Output: false
Explanation: The first three characters "app" match, and the second string is shorter (in size.) According to lexicographical rules "apple" > "app", because 'l' > '∅', where '∅' is defined as the blank character which is less than any other character (More info).
```
##### Constraints:
* 1 <= words.length <= 100
* 1 <= words[i].length <= 20
* order.length == 26
* All characters in words[i] and order are English lowercase letters.

### Solution:
```java
class Solution {
    public boolean isAlienSorted(String[] words, String order) {
        int[] mp = new int[26];
        for(int i = 0; i < order.length(); i++){
            mp[order.charAt(i) - 'a'] = i;
        }
        for(int i = 0; i < words.length - 1; i++){
            int k = 0;
            int kn = words[i].length();
            int ln = words[i + 1].length();
            int minDiff = 0;
            while(k < kn && k < ln){
                int diff = mp[words[i].charAt(k) - 'a'] - mp[words[i + 1].charAt(k) - 'a'];
                minDiff = Math.min(diff,minDiff);
                if(diff < 0) break;
                if(diff > 0) return false;
                k++;
            }
            if(minDiff == 0 && kn > ln) return false; 
        }
        
        return true;
    }
}
```