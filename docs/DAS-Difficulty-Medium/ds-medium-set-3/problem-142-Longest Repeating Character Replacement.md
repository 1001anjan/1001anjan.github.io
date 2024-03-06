---
layout: default
title: Longest Repeating Character Replacement
parent: Medium Set 3
grand_parent: DSA Medium
nav_order: 42
permalink: /problem-142-Longest Repeating Character Replacement/
---
# Longest Repeating Character Replacement
You are given a string s and an integer k. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most k times.

Return the length of the longest substring containing the same letter you can get after performing the above operations.

##### Example 1:
```markdown
Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa.
```
##### Example 2:
```markdown
Input: s = "AABABBA", k = 1
Output: 4
Explanation: Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
```
##### Constraints:
* 1 <= s.length <= 10^5
* s consists of only uppercase English letters.
* 0 <= k <= s.length

### Solution:
##### Time Limit Exceeded O(n^2) time complexity

```java
class Solution {
    public int characterReplacement(String s, int k) {
        int max = -1;
        int len = s.length();
        for(int i = 0; i < len; i++){
            char ch = s.charAt(i);
            int k1 = k;
            int n1 = 1;
            int j = i + 1;            
            // max in right side
            while(j < len){
                if(ch != s.charAt(j)) k1 --;
                if(k1 < 0) break;
                n1 ++;
                j++;
            }
            // checking middele to left
            if(j == len && k1 > 0){
                j = i - 1;
                while(j >= 0){
                    if(ch != s.charAt(j)) k1 --;
                    if(k1 < 0) break;
                    n1 ++;
                    j--;
                }
            }


            // finding max in left side
             int n2 = 1;
             j = i - 1;
             k1 = k;
             while(j >= 0){
                if(ch != s.charAt(j)) k1 --;
                if(k1 < 0) break;
                n2 ++;
                j--;
            }
            // checking middle to right
            if(j == 0 && k1 > 0){
                j = i + 1;
                while(j < len){
                    if(ch != s.charAt(j)) k1 --;
                    if(k1 < 0) break;
                    n2 ++;
                    j++;
                } 
            }
            
            max = Math.max(max, Math.max(n1, n2));
        }

        return max;
    }
}
```

##### Find different approach to solve the problem here [Leet Code explanation](https://leetcode.com/problems/longest-repeating-character-replacement/solutions/2805777/longest-repeating-character-replacement/)
```java
class Solution {
    public int characterReplacement(String s, int k) {
        int start = 0;
        int maxFrequency = 0;
        int maxWindowSize = 0;
        int[] frequencyMap = new int[26];

        for(int end = 0; end < s.length(); end++){
            int charIndex = s.charAt(end) - 'A';
            frequencyMap[charIndex]++;
            maxFrequency = Math.max(maxFrequency, frequencyMap[charIndex]);
            // move the start pointer towards right if the current
            // window is invalid
            // validity condition windowSize - maxFrequency <= k
            boolean isValid = (end - start + 1) - maxFrequency <= k;
            if(!isValid){
                charIndex = s.charAt(start) - 'A';
                frequencyMap[charIndex]--;
                start ++;
            }
            
            maxWindowSize = end - start + 1;
        }

        return maxWindowSize;
    }
}
```