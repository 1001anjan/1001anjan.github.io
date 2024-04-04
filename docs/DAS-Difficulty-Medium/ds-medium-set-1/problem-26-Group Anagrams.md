---
layout: default
title: Group Anagrams
parent: Medium Set 1
grand_parent: DSA Medium
nav_order: 26
permalink: /problem-26-Group Anagrams/
---
# Group Anagrams
Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

##### Example 1:
```markdown
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```
##### Example 2:
```markdown
Input: strs = [""]
Output: [[""]]
```
##### Example 3:
```markdown
Input: strs = ["a"]
Output: [["a"]]
```
##### Constraints:
* 1 <= strs.length <= 104
* 0 <= strs[i].length <= 100
* strs[i] consists of lowercase English letters.

### Solution:
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        int[][] dp = new int[strs.length][26];
        
        for(int i = 0; i < strs.length; i++){
            for(char ch : strs[i].toCharArray()){
                dp[i][ch - 'a']++;
            }
        }

        List<List<String>> ans = new ArrayList<>();
        Set<String> used = new HashSet<>();
        for(int i = 0; i < strs.length; i++){
            if(!used.add(strs[i])) continue;
            List<String> group = new ArrayList<>();
            group.add(strs[i]);
            for(int j = i + 1; j < dp.length; j++){
                if(i == j) continue;
                int k = 0;
                while(k < 26){
                    if(dp[i][k] != dp[j][k]) break;
                    k++;
                }
                if(k == 26){
                    used.add(strs[j]);
                    group.add(strs[j]);
                } 
            }
            ans.add(group);
        }

        return ans;
    }
}
```

```java
class Solution {
        public List<List<String>> groupAnagrams(String[] strs) {
            if (strs == null || strs.length == 0) return new ArrayList<>();
            Map<String, List<String>> map = new HashMap<>();
            for (String s : strs) {
                char[] ca = new char[26];
                for (char c : s.toCharArray()) ca[c - 'a']++;
                String keyStr = String.valueOf(ca);
                if (!map.containsKey(keyStr)) map.put(keyStr, new ArrayList<>());
                map.get(keyStr).add(s);
            }
            return new ArrayList<>(map.values());
    }
}
```