---
layout: default
title: Truncate Sentence
parent: Easy Set 9
grand_parent: DSA Easy Difficulty
nav_order: 27
permalink: /problem-277-Truncate-Sentence/
---
# Truncate Sentence
A sentence is a list of words that are separated by a single space with no leading or trailing spaces. Each of the words consists of only uppercase and lowercase English letters (no punctuation).

For example, "Hello World", "HELLO", and "hello world hello world" are all sentences.
You are given a sentence s and an integer k. You want to truncate s such that it contains only the first k words. Return s after truncating it.

##### Example 1:
```markdown
Input: s = "Hello how are you Contestant", k = 4
Output: "Hello how are you"
Explanation:
The words in s are ["Hello", "how" "are", "you", "Contestant"].
The first 4 words are ["Hello", "how", "are", "you"].
Hence, you should return "Hello how are you".
```
##### Example 2:
```markdown
Input: s = "What is the solution to this problem", k = 4
Output: "What is the solution"
Explanation:
The words in s are ["What", "is" "the", "solution", "to", "this", "problem"].
The first 4 words are ["What", "is", "the", "solution"].
Hence, you should return "What is the solution".
```
##### Example 3:
```markdown
Input: s = "chopper is not a tanuki", k = 5
Output: "chopper is not a tanuki"
```
##### Constraints:
* 1 <= s.length <= 500
* k is in the range [1, the number of words in s].
* s consist of only lowercase and uppercase English letters and spaces.
* The words in s are separated by a single space.
* There are no leading or trailing spaces.

### Solution:
```java
class Solution {
    public String truncateSentence(String s, int k) {
        String[] wrd = s.split(" ");
        int i = 0;
        StringBuilder sb = new StringBuilder();
        do{
            sb.append(wrd[i]).append(" ");
            i++;
        }while(i < k && i < wrd.length);
        return sb.substring(0,sb.length() - 1).toString();
    }
}
```
####### Naturally faster
```java
class Solution {
    public String truncateSentence(String s, int k) {
        StringBuilder sb = new StringBuilder();
        int countSpaces = 0;
        
        for(char curr : s.toCharArray()) {   
            if(curr == ' ') {
                countSpaces++;
            }
            if(countSpaces == k) break;
            sb.append(curr);
        }
        
      return sb.toString();
    }
}
```