---
layout: default
title: Check if the Sentence Is Pangram
parent: Easy Set 9
grand_parent: DSA Easy
nav_order: 30
permalink: /problem-280-Check-if-the-Sentence-Is-Pangram/
---
# Check if the Sentence Is Pangram
A pangram is a sentence where every letter of the English alphabet appears at least once.

Given a string sentence containing only lowercase English letters, return true if sentence is a pangram, or false otherwise.

##### Example 1:
```markdown
Input: sentence = "thequickbrownfoxjumpsoverthelazydog"
Output: true
Explanation: sentence contains at least one of every letter of the English alphabet.
```
##### Example 2:
```markdown
Input: sentence = "leetcode"
Output: false
```
##### Constraints:
* 1 <= sentence.length <= 1000
* sentence consists of lowercase English letters.

### Solution:
```java
class Solution {
    public boolean checkIfPangram(String sentence) {
        Set<Character> s = new HashSet();
        for(char c : sentence.toCharArray()){
            s.add(c);
        }
        
        return s.size() == 26;
    }
}
```
##### Execution wise faster 
```java
class Solution {
    public boolean checkIfPangram(String sentence) {
        boolean[] dp = new boolean[26];
        for(char c : sentence.toCharArray()){
            dp[c - 'a'] = true;
        }
        
        for(boolean d : dp){
            if(!d) return false;
        }
        return true;
    }
}
```
##### Even faster execution 
```java
class Solution {
    public boolean checkIfPangram(String sentence) {
        if(sentence.length() < 26){
            return false;
        }
        else{
            String str = "abcdefghijklmnopqrstuvwxyz";
            for(int i=0;i < str.length();i++){
                if(sentence.indexOf(str.charAt(i)) == -1){
                    return false;
                }
            }
            return true;
        }
        
    }
}
```