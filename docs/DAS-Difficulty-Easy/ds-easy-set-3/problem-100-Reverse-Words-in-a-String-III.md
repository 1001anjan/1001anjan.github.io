---
layout: default
title: Reverse Words in a String III
parent: Easy Set 3
grand_parent: DSA Easy Difficulty
nav_order: 37
permalink: /problem-100-Reverse-Words-in-a-String-III/
---
# Reverse Words in a String III

Given a string s, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

##### Example 1:
```markdown
Input: s = "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```
##### Example 2:
```markdown
Input: s = "God Ding"
Output: "doG gniD"
```
##### Constraints:
* 1 <= s.length <= 5 * 104
* s contains printable ASCII characters.
* s does not contain any leading or trailing spaces.
* There is at least one word in s.
* All the words in s are separated by a single space.

### Solution:
```java
class Solution {
    public String reverseWords(String s) {
        char[] str = s.toCharArray();
        int i = 0;
        while(i<str.length){
            
            if(str[i] != ' '){
               int l = i;
                int u = i;
                while(u<str.length){
                    if(str[u] == ' ') break;
                    u++;
                }
                i = u;
                u--;
                while(l<u){
                    char ch = str[l];
                    str[l] = str[u];
                    str[u] = ch;
                    l++;
                    u--;
                }
            }else
                i++;
        }
        return new String(str);
    }
}
```
```java
public class Solution {
    public String reverseWords(String s) {
        String words[] = s.split(" ");
        StringBuilder res=new StringBuilder();
        for (String word: words)
            res.append(new StringBuffer(word).reverse().toString() + " ");
        return res.toString().trim();
    }
}
```
