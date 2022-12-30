---
layout: default
title: String Matching in an Array
parent: Easy Set 6
grand_parent: DSA Easy Difficulty
nav_order: 25
permalink: /problem-185-String-Matching-in-an-Array/
---
# String Matching in an Array
Given an array of string words. Return all strings in words which is substring of another word in any order.

String words[i] is substring of words[j], if can be obtained removing some characters to left and/or right side of words[j].

##### Example 1:
```markdown
Input: words = ["mass","as","hero","superhero"]
Output: ["as","hero"]
Explanation: "as" is substring of "mass" and "hero" is substring of "superhero".
["hero","as"] is also a valid answer.
```
##### Example 2:
```markdown
Input: words = ["leetcode","et","code"]
Output: ["et","code"]
Explanation: "et", "code" are substring of "leetcode".
```
##### Example 3:
```markdown
Input: words = ["blue","green","bu"]
Output: []
```
##### Constraints:
* 1 <= words.length <= 100
* 1 <= words[i].length <= 30
* words[i] contains only lowercase English letters.
* It's guaranteed that words[i] will be unique.

### Solution:
```java
class Solution {
    public List<String> stringMatching(String[] words) {
        List<String>ans = new ArrayList<>();
        for(int i=0; i<words.length; i++){
            String s = words[i];
            for(int j=0; j<words.length; j++){
                if(i == j){
                    continue;
                }
                if(words[j].contains(s)){
                    ans.add(s);
                    break;
                }
            }
        }
        return ans;
    }
}
```