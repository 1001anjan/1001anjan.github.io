---
layout: default
title: Most Common Word
parent: Easy Set 13
grand_parent: DSA Easy Difficulty
nav_order: 27
permalink: /problem-397-Most Common Word/
---
# Most Common Word
Given a string paragraph and a string array of the banned words banned, return the most frequent word that is not banned. It is guaranteed there is at least one word that is not banned, and that the answer is unique.

The words in paragraph are case-insensitive and the answer should be returned in lowercase.

##### Example 1:
```markdown
Input: paragraph = "Bob hit a ball, the hit BALL flew far after it was hit.", banned = ["hit"]
Output: "ball"
Explanation:
"hit" occurs 3 times, but it is a banned word.
"ball" occurs twice (and no other word does), so it is the most frequent non-banned word in the paragraph.
Note that words in the paragraph are not case sensitive,
that punctuation is ignored (even if adjacent to words, such as "ball,"),
and that "hit" isn't the answer even though it occurs more because it is banned.
```
##### Example 2:
```markdown
Input: paragraph = "a.", banned = []
Output: "a"
```
##### Constraints:
* 1 <= paragraph.length <= 1000
* paragraph consists of English letters, space ' ', or one of the symbols: "!?',;.".
* 0 <= banned.length <= 100
* 1 <= banned[i].length <= 10
* banned[i] consists of only lowercase English letters.

### Solution
```java
class Solution {
    public String mostCommonWord(String paragraph, String[] banned) {
        Set<String> set = new HashSet<>();
        for(String str : banned) set.add(str);
        HashMap<String,Integer> mp = new HashMap<>();
        
        int i = 0;
        int size = paragraph.length();
        char[] str = paragraph.toCharArray();
        StringBuilder sb = new StringBuilder();
        while(i < size){
            while(i < size && str[i] == ' ') i++;
            sb.setLength(0);
            while(i < size){
                if(Character.isLetter(str[i])) sb.append(Character.toLowerCase(str[i]));
                else
                break;
                i++;
            }
            String s = sb.toString();
            if(sb.length() > 0 && !set.contains(s)) 
                mp.put(s, mp.getOrDefault(s,0) + 1);
            i++;
        }
        int max = Collections.max(mp.values());
        for(String key : mp.keySet()){
            if(mp.get(key) == max) return key;
        }
        return null;
    }
}
```