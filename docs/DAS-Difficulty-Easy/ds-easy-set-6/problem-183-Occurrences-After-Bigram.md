---
layout: default
title: Occurrences After Bigram
parent: Easy Set 6
grand_parent: DSA Easy Difficulty
nav_order: 23
permalink: /problem-183-Occurrences-After-Bigram/
---
# Occurrences After Bigram
Given two strings first and second, consider occurrences in some text of the form "first second third", where second comes immediately after first, and third comes immediately after second.

Return an array of all the words third for each occurrence of "first second third".

##### Example 1:
```markdown
Input: text = "alice is a good girl she is a good student", first = "a", second = "good"
Output: ["girl","student"]
```
##### Example 2:
```markdown
Input: text = "we will we will rock you", first = "we", second = "will"
Output: ["we","rock"]
```
##### Constraints:
* 1 <= text.length <= 1000
* text consists of lowercase English letters and spaces.
* All the words in text a separated by a single space.
* 1 <= first.length, second.length <= 10
* first and second consist of lowercase English letters.

### Solution: 
```java
class Solution {
    public String[] findOcurrences(String text, String first, String second) {
        String[] words = text.split(" ");
        ArrayList<String> ans = new ArrayList<>();
       
        for( int i = 0; i < words.length - 2; i++){
            if(words[i].equals(first) && words[i+1].equals(second))
                ans.add(words[i+2]);
        }
        
        String[] res = new String[ans.size()];
        
        return ans.toArray(res);
    }
}
```