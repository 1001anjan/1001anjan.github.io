---
layout: default
title: Decode the Message
parent: Data Structure Easy Set 12
grand_parent: Data Structure
nav_order: 24
permalink: /problem-364-Decode the Message/
---
# Decode the Message
You are given the strings key and message, which represent a cipher key and a secret message, respectively. The steps to decode message are as follows:

1. Use the first appearance of all 26 lowercase English letters in key as the order of the substitution table.
2. Align the substitution table with the regular English alphabet.
3. Each letter in message is then substituted using the table.
4. Spaces ' ' are transformed to themselves.
* For example, given key = "happy boy" (actual key would have at least one instance of each letter in the alphabet), we have the partial substitution table of ('h' -> 'a', 'a' -> 'b', 'p' -> 'c', 'y' -> 'd', 'b' -> 'e', 'o' -> 'f').
Return the decoded message.

##### Example 1:
![](../../assets/images/ds/ex1new4.jpeg)
```markdown
Input: key = "the quick brown fox jumps over the lazy dog", message = "vkbs bs t suepuv"
Output: "this is a secret"
Explanation: The diagram above shows the substitution table.
It is obtained by taking the first appearance of each letter in "the quick brown fox jumps over the lazy dog".
```
##### Example 2:
![](../../assets/images/ds/ex2new.jpeg)
```markdown
Input: key = "eljuxhpwnyrdgtqkviszcfmabo", message = "zwx hnfx lqantp mnoeius ycgk vcnjrdb"
Output: "the five boxing wizards jump quickly"
Explanation: The diagram above shows the substitution table.
It is obtained by taking the first appearance of each letter in "eljuxhpwnyrdgtqkviszcfmabo".
```
##### Constraints:
* 26 <= key.length <= 2000
* key consists of lowercase English letters and ' '.
* key contains every letter in the English alphabet ('a' to 'z') at least once.
* 1 <= message.length <= 2000
* message consists of lowercase English letters and ' '.

### Solution: 
```java
class Solution {
    public String decodeMessage(String key, String message) {
        char[] dp = new char[26];
        char c = 'a';
        for(char ch : key.toCharArray()){
            int index = ch - 'a';
            if(ch != ' ' && dp[index] == 0){
                dp[index] = c++;
            } 
        }
        StringBuilder sb = new StringBuilder();
        for(char ch : message.toCharArray()){
            if(ch == ' '){
                sb.append(ch);
            } 
            else{
                sb.append(dp[ch - 'a']);
            }
        }
        return sb.toString();
    }
}
```