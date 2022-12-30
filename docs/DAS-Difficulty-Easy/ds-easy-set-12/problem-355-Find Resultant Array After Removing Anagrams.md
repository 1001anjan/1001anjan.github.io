---
layout: default
title: Find Resultant Array After Removing Anagrams
parent: Easy Set 12
grand_parent: DSA Easy Difficulty
nav_order: 15
permalink: /problem-355-Find Resultant Array After Removing Anagrams/
---
# Find Resultant Array After Removing Anagrams
You are given a 0-indexed string array words, where words[i] consists of lowercase English letters.

In one operation, select any index i such that 0 < i < words.length and words[i - 1] and words[i] are anagrams, and delete words[i] from words. Keep performing this operation as long as you can select an index that satisfies the conditions.

Return words after performing all operations. It can be shown that selecting the indices for each operation in any arbitrary order will lead to the same result.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase using all the original letters exactly once. For example, "dacb" is an anagram of "abdc".

##### Example 1:
```markdown
Input: words = ["abba","baba","bbaa","cd","cd"]
Output: ["abba","cd"]
Explanation:
One of the ways we can obtain the resultant array is by using the following operations:
- Since words[2] = "bbaa" and words[1] = "baba" are anagrams, we choose index 2 and delete words[2].
  Now words = ["abba","baba","cd","cd"].
- Since words[1] = "baba" and words[0] = "abba" are anagrams, we choose index 1 and delete words[1].
  Now words = ["abba","cd","cd"].
- Since words[2] = "cd" and words[1] = "cd" are anagrams, we choose index 2 and delete words[2].
  Now words = ["abba","cd"].
  We can no longer perform any operations, so ["abba","cd"] is the final answer.
```
##### Example 2:
```markdown
Input: words = ["a","b","c","d","e"]
Output: ["a","b","c","d","e"]
Explanation:
No two adjacent strings in words are anagrams of each other, so no operations are performed.
```
##### Constraints:
* 1 <= words.length <= 100
* 1 <= words[i].length <= 10
* words[i] consists of lowercase English letters.

### Solution:
```java
class Solution {
    public List<String> removeAnagrams(String[] words) {
        List<String> ans = new ArrayList<>();
        int[] dp = new int[26];
        ans.add(words[0]);
        for(char ch : words[0].toCharArray()) dp[ch - 'a']++;
        
        for(int i = 1; i < words.length; i++){
            int[] dpp = getAnagramsMap(words[i]);
            boolean flag = true;
            for(int j = 0; j < 26; j++){
                if(dpp[j] != dp[j]) flag = false;
                dp[j] = dpp[j];
            }
            if(!flag) ans.add(words[i]);
        }
        return ans;
    }
    
    public int[] getAnagramsMap(String str){
        int[] dp = new int[26];
        for(char ch : str.toCharArray()) dp[ch - 'a']++;
        return dp;
    }
}
```

##### Anotherway 
```java
class Solution {
    public List<String> removeAnagrams(String[] words) {
        int low = 0;
        List<String> ans = new ArrayList<>();
        
        int[] prev = count(words[low]);
        for(int i=1;i<words.length;i++){
            
            int[] curr = count(words[i]);
            if(Arrays.equals(prev,curr)){
                continue;
            }
            ans.add(words[low]);
            low = i;
            prev = count(words[low]);
        }
        ans.add(words[low]);
        return ans;
    }
    private int[] count(String s){
        int[] c = new int[26];
        int n = s.length();
        for(int i=0;i<n;i++){
            c[s.charAt(i)-'a']++;
        }
        return c;
    }
}
```