---
layout: default
title: Number of Valid Words in a Sentence
parent: Easy Set 11
grand_parent: DSA Easy Difficulty
nav_order: 6
permalink: /problem-316-Number of Valid Words in a Sentence/
---
# Number of Valid Words in a Sentence
A sentence consists of lowercase letters ('a' to 'z'), digits ('0' to '9'), hyphens ('-'), punctuation marks ('!', '.', and ','), and spaces (' ') only. Each sentence can be broken down into one or more tokens separated by one or more spaces ' '.

A token is a valid word if all three of the following are true:

* It only contains lowercase letters, hyphens, and/or punctuation (no digits).
* There is at most one hyphen '-'. If present, it must be surrounded by lowercase characters ("a-b" is valid, but "-ab" and "ab-" are not valid).
* There is at most one punctuation mark. If present, it must be at the end of the token ("ab,", "cd!", and "." are valid, but "a!b" and "c.," are not valid).

Examples of valid words include "a-b.", "afad", "ba-c", "a!", and "!".

Given a string sentence, return the number of valid words in sentence.

#### Example 1:
```markdown
Input: sentence = "cat and  dog"
Output: 3
Explanation: The valid words in the sentence are "cat", "and", and "dog".
```
##### Example 2:
```markdown
Input: sentence = "!this  1-s b8d!"
Output: 0
Explanation: There are no valid words in the sentence.
"!this" is invalid because it starts with a punctuation mark.
"1-s" and "b8d" are invalid because they contain digits.
```
##### Example 3:
```markdown
Input: sentence = "alice and  bob are playing stone-game10"
Output: 5
Explanation: The valid words in the sentence are "alice", "and", "bob", "are", and "playing".
"stone-game10" is invalid because it contains digits.
```
##### Constraints:
* 1 <= sentence.length <= 1000
* sentence only contains lowercase English letters, digits, ' ', '-', '!', '.', and ','.
* There will be at least 1 token.

### Solution:
```java
class Solution {
    public int countValidWords(String sentence) {
        int count = 0;
        String[] words = sentence.trim().split("\\s+");
        for(String str : words){
            int hypens = 0;
            int n = str.length();
            int i = 0;
            
            while(i < n){
                char ch = str.charAt(i);
                if(Character.isDigit(ch)){
                    break;
                } 
                if(ch == '-'){
                    if(i == 0 || i == n - 1) break;
                    if(!Character.isLetter(str.charAt(i-1)) || !Character.isLetter(str.charAt(i+1))) break;
                    hypens++;
                }else if(ch == '!' || ch == '.' || ch == ','){
                    if(i != n - 1) break; 
                }
                i++;
            }
            
            if(hypens <= 1 && i == n) count++;
        }
        
        return count;
    }
}
```
##### Improvement
```java
class Solution {
    public int countValidWords(String sentence) {
        int count = 0;
        String[] words = sentence.split(" ");
        for(String str : words){
            int n = str.length();
            if(n == 0) continue;
            int hypens = 0;
            int i = 0;
            
            while(i < n){
                char ch = str.charAt(i);
                if(Character.isDigit(ch)){
                    break;
                } 
                if(ch == '-'){
                    hypens++;
                    if(i == 0 || i == n - 1 || hypens > 1) break;
                    if(!Character.isLetter(str.charAt(i-1)) || !Character.isLetter(str.charAt(i+1))) break;
                }else if(ch == '!' || ch == '.' || ch == ','){
                    if(i != n - 1) break; 
                }
                i++;
            }
            
            if(i == n) count++;
        }
        
        return count;
    }
}
```