---
layout: default
title: Goat Latin
parent: Easy Set 5
grand_parent: DSA Easy Difficulty
nav_order: 1
permalink: /problem-131-Goat-Latin/
---
# Goat Latin
You are given a string sentence that consist of words separated by spaces. Each word consists of lowercase and uppercase letters only.

We would like to convert the sentence to "Goat Latin" (a made-up language similar to Pig Latin.) The rules of Goat Latin are as follows:

* If a word begins with a vowel ('a', 'e', 'i', 'o', or 'u'), append "ma" to the end of the word.
** For example, the word "apple" becomes "applema".
* If a word begins with a consonant (i.e., not a vowel), remove the first letter and append it to the end, then add "ma".
** For example, the word "goat" becomes "oatgma".
* Add one letter 'a' to the end of each word per its word index in the sentence, starting with 1.
** For example, the first word gets "a" added to the end, the second word gets "aa" added to the end, and so on.

Return the final sentence representing the conversion from sentence to Goat Latin.

##### Example 1:
```markdown
Input: sentence = "I speak Goat Latin"
Output: "Imaa peaksmaaa oatGmaaaa atinLmaaaaa"
```
##### Example 2:
```markdown
Input: sentence = "The quick brown fox jumped over the lazy dog"
Output: "heTmaa uickqmaaa rownbmaaaa oxfmaaaaa umpedjmaaaaaa overmaaaaaaa hetmaaaaaaaa azylmaaaaaaaaa ogdmaaaaaaaaaa"
```
##### Constraints:
* 1 <= sentence.length <= 150
* sentence consists of English letters and spaces.
* sentence has no leading or trailing spaces.
* All the words in sentence are separated by a single space.

### Solution:
```java
class Solution {
    public String toGoatLatin(String sentence) {
        StringBuilder sb = new StringBuilder();
        StringBuilder suf = new StringBuilder();
        suf.append('a');
        String[] words = sentence.split("\\s+");
        for(String s : words){
            if(isVowel(s.charAt(0))){
                sb.append(s);
            }else{
                sb.append(s.substring(1,s.length()));
                sb.append(s.charAt(0));
            }
            sb.append("ma");
            sb.append(suf);
            sb.append(" ");
            suf.append("a");
        }
        return sb.toString().trim();
    }
    
    public boolean isVowel(char c){
        switch(c){
            case 'a','e','i','o','u','A','E','I','O','U': return true;
            default: return false;
        }
    }
}
```