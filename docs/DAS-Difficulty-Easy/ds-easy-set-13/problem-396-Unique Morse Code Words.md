---
layout: default
title: Unique Morse Code Words
parent: Easy Set 13
grand_parent: DSA Easy
nav_order: 26
permalink: /problem-396-Unique Morse Code Words/
---
# Unique Morse Code Words
International Morse Code defines a standard encoding where each letter is mapped to a series of dots and dashes, as follows:

* 'a' maps to ".-",
* 'b' maps to "-...",
* 'c' maps to "-.-.", and so on.
For convenience, the full table for the 26 letters of the English alphabet is given below:

```markdown
[".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]
```
Given an array of strings words where each word can be written as a concatenation of the Morse code of each letter.

* For example, "cab" can be written as "-.-..--...", which is the concatenation of "-.-.", ".-", and "-...". We will call such a concatenation the transformation of a word.
Return the number of different transformations among all words we have.

##### Example 1:
```markdown
Input: words = ["gin","zen","gig","msg"]
Output: 2
Explanation: The transformation of each word is:
"gin" -> "--...-."
"zen" -> "--...-."
"gig" -> "--...--."
"msg" -> "--...--."
There are 2 different transformations: "--...-." and "--...--.".
```
##### Example 2:
```markdown
Input: words = ["a"]
Output: 1
```
##### Constraints:
* 1 <= words.length <= 100
* 1 <= words[i].length <= 12
* words[i] consists of lowercase English letters.

### Solution:
```java
class Solution {
    public int uniqueMorseRepresentations(String[] words) {
        String[] MORSE = new String[]{".-","-...","-.-.","-..",".","..-.","--.",
                         "....","..",".---","-.-",".-..","--","-.",
                         "---",".--.","--.-",".-.","...","-","..-",
                         "...-",".--","-..-","-.--","--.."};

        Set<String> seen = new HashSet();
        for (String word: words) {
            StringBuilder code = new StringBuilder();
            for (char c: word.toCharArray())
                code.append(MORSE[c - 'a']);
            seen.add(code.toString());
        }

        return seen.size();
    }
}
```