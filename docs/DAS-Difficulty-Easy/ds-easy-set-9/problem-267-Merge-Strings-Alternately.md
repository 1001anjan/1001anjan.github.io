---
layout: default
title: Merge Strings Alternately
parent: Easy Set 9
grand_parent: DSA Easy
nav_order: 17
permalink: /problem-267-Merge-Strings-Alternately/
---
# Merge Strings Alternately
You are given two strings word1 and word2. Merge the strings by adding letters in alternating order, starting with word1. If a string is longer than the other, append the additional letters onto the end of the merged string.

Return the merged string.

##### Example 1:
```markdown
Input: word1 = "abc", word2 = "pqr"
Output: "apbqcr"
Explanation: The merged string will be merged as so:
word1:  a   b   c
word2:    p   q   r
merged: a p b q c r
```
##### Example 2:
```markdown
Input: word1 = "ab", word2 = "pqrs"
Output: "apbqrs"
Explanation: Notice that as word2 is longer, "rs" is appended to the end.
word1:  a   b
word2:    p   q   r   s
merged: a p b q   r   s
```
##### Example 3:
```markdown
Input: word1 = "abcd", word2 = "pq"
Output: "apbqcd"
Explanation: Notice that as word1 is longer, "cd" is appended to the end.
word1:  a   b   c   d
word2:    p   q
merged: a p b q c   d
```
##### Constraints:
* 1 <= word1.length, word2.length <= 100
* word1 and word2 consist of lowercase English letters.

### Solution:
```java
class Solution {
    public String mergeAlternately(String word1, String word2) {
        StringBuilder sb = new StringBuilder();
        int i = 0, j = 0;
        boolean stc = true;
        while(i < word1.length() && j < word2.length()){
            if(stc){
                sb.append(word1.charAt(i));
                i++;
            }else{
                sb.append(word2.charAt(j));
                j++;
            }
            stc = !stc;  
        }
        while(i < word1.length()){
            sb.append(word1.charAt(i));
            i++; 
        }
        while(j < word2.length()){
            sb.append(word2.charAt(j));
            j++; 
        }
        
        return sb.toString();
    }
}
```
#### Another way
```java
class Solution {
    public String mergeAlternately(String word1, String word2) {
        int n=Math.max(word1.length(),word2.length());
            StringBuilder res=new StringBuilder();
            for(int i=0;i<n;i++){
                    if(i<word1.length())res.append(word1.charAt(i));
                    if(i<word2.length())res.append(word2.charAt(i));
            }
            return res.toString();
    }
}
```