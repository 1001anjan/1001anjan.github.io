---
layout: default
title: Word Break
parent: Data Structure Medium Set 2
grand_parent: Data Structure
nav_order: 36
permalink: /problem-86-Word Break/
---
# Word Break
Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.

Note that the same word in the dictionary may be reused multiple times in the segmentation.

##### Example 1:
```markdown
Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```
##### Example 2:
```markdown
Input: s = "applepenapple", wordDict = ["apple","pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
Note that you are allowed to reuse a dictionary word.
```
##### Example 3:
```markdown
Input: s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
Output: false
```
##### Constraints:
* 1 <= s.length <= 300
* 1 <= wordDict.length <= 1000
* 1 <= wordDict[i].length <= 20
* s and wordDict[i] consist of only lowercase English letters.
* All the strings of wordDict are unique.

### Solution
#### Time Limit Exceeded
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        return processWordBreak(s, 0, wordDict);
    }

    public boolean processWordBreak(String s, int index, List<String> words){
        if(index >= s.length()) return true;
        for(String str : words){
            if(index + str.length() <= s.length() && s.substring(index, index + str.length()).equals(str)){
                  if(processWordBreak(s, index + str.length(), words)) return true;
            }
        }

        return false;
    }
}
```
##### Dynamic Programming
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int n = s.length();
        boolean[] dp = new boolean[n + 1];
        Set<String> set = new HashSet<>(wordDict);
        dp[0] = true;
        
        for(int i = 1; i <= n; i++){
            for(int j = 0; j <= i; j++){
                if(dp[j] && set.contains(s.substring(j,i))){
                    dp[i] = true;
                    break;
                }
            }
        }

        return dp[n];
    }

}
```