---
layout: default
title: Uncommon Words from Two Sentences
parent: Data Structure Easy Set 5
grand_parent: Data Structure
nav_order: 11
permalink: /problem-141-Uncommon-Words-from-Two-Sentences/
---
# Uncommon Words from Two Sentences

A sentence is a string of single-space separated words where each word consists only of lowercase letters.

A word is uncommon if it appears exactly once in one of the sentences, and does not appear in the other sentence.

Given two sentences s1 and s2, return a list of all the uncommon words. You may return the answer in any order.

##### Example 1:
```markdown
Input: s1 = "this apple is sweet", s2 = "this apple is sour"
Output: ["sweet","sour"]
```
##### Example 2:
```markdown
Input: s1 = "apple apple", s2 = "banana"
Output: ["banana"]
```
##### Constraints:
* 1 <= s1.length, s2.length <= 200
* s1 and s2 consist of lowercase English letters and spaces.
* s1 and s2 do not have leading or trailing spaces.
* All the words in s1 and s2 are separated by a single space.

### Solution:
```java
class Solution {
    public String[] uncommonFromSentences(String s1, String s2) {
        Map<String,Integer> map = new HashMap<String,Integer>();
        for(String w : s1.split("\\s+")){
            map.put(w,map.getOrDefault(w,0)+1);
        }
        for(String w : s2.split("\\s+")){
            map.put(w,map.getOrDefault(w,0)+1);
        }
        List<String> ans = new ArrayList<>();
        for(String s: map.keySet()){
            if(map.get(s) == 1) ans.add(s);
        }
        return ans.toArray(new String[ans.size()]);
    }
}
```
```java
class Solution {
    public String[] uncommonFromSentences(String A, String B) {
        Map<String, Integer> count = new HashMap();
        for (String word: A.split(" "))
            count.put(word, count.getOrDefault(word, 0) + 1);
        for (String word: B.split(" "))
            count.put(word, count.getOrDefault(word, 0) + 1);

        List<String> ans = new LinkedList();
        for (String word: count.keySet())
            if (count.get(word) == 1)
                ans.add(word);

        return ans.toArray(new String[ans.size()]);
    }
}
```