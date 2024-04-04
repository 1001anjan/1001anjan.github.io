---
layout: default
title: Keyboard Row
parent: Easy Set 3
grand_parent: DSA Easy
nav_order: 26
permalink: /problem-89-Keyboard-Row/
---
# Keyboard Row
Given an array of strings words, return the words that can be typed using letters of the alphabet on only one row of American keyboard like the image below.

In the American keyboard:

* the first row consists of the characters "qwertyuiop",
* the second row consists of the characters "asdfghjkl", and
* the third row consists of the characters "zxcvbnm".

##### Example 1:
```markdown
Input: words = ["Hello","Alaska","Dad","Peace"]
Output: ["Alaska","Dad"]
```
##### Example 2:
```markdown
Input: words = ["omk"]
Output: []
```
##### Example 3:
```markdown
Input: words = ["adsdf","sfd"]
Output: ["adsdf","sfd"]
```
##### Constraints:

* 1 <= words.length <= 20
* 1 <= words[i].length <= 100
* words[i] consists of English letters (both lowercase and uppercase). 

```java
class Solution {
    public String[] findWords(String[] words) {
        ArrayList<String> str = new ArrayList<String>();
        String[] keys = new String[3];
        keys[0] = "QqWwEeRrTtYyUuIiOoPp";
        keys[1] = "AaSsDdFfGgHhJjKkLl";
        keys[2] = "ZzXxCcVvBbNnMm";
        for(String word : words){
            char ch = word.charAt(0);
            int key = -1;
            if(keys[0].contains(String.valueOf(ch))) key = 0;
            if(keys[1].contains(String.valueOf(ch))) key = 1;
            if(keys[2].contains(String.valueOf(ch))) key = 2;
            if(key != -1){
                int i=1;
                for(; i<word.length(); i++){
                  if(!keys[key].contains(String.valueOf(word.charAt(i)))) break;
                }
                if(i == word.length()) str.add(word);
            }    
        }
        return str.toArray(new String[str.size()]);   
    }
}
```