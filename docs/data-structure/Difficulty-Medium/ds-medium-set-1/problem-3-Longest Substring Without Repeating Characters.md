---
layout: default
title: Longest Substring Without Repeating Characters
parent: Data Structure Medium Set 1
grand_parent: Data Structure
nav_order: 3
permalink: /problem-3-Longest Substring Without Repeating Characters/
---
# Longest Substring Without Repeating Characters
Given a string s, find the length of the longest
substring
without repeating characters.

##### Example 1:
```markdown
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```
##### Example 2:
```markdown
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```
##### Example 3:
```markdown
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```
##### Constraints:
* 0 <= s.length <= 5 * 104
* s consists of English letters, digits, symbols and spaces.

### Solution: 
```java
class Solution {
    public int lengthOfLongestSubstring(String str) {
        Set<Character> set = new HashSet<>();
        int s = 0, e = 0, max = 0, curr = 0;
        while(e < str.length()){
            char ch = str.charAt(e);
            if(set.add(ch)){
                curr++;
                e++;
            }else{
                while(str.charAt(s) != ch) {
                    set.remove(str.charAt(s));
                    s++;
                }
                s++;
                curr = e - s + 1;
                e++;
            }
            max = Math.max(max, curr);
        }

        return max;
    }
}
```
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int max = 0;
        int tmax;
        
        for(int i=0; i<s.length(); i++){
            tmax= 1;
            HashSet<Character>  set = new HashSet();
            set.add(s.charAt(i));
            for(int j= i+1; j<s.length(); j++){
                if(set.contains(s.charAt(j))) break;
                tmax++;
                set.add(s.charAt(j));

            }
            if(tmax>max)
                max = tmax;
        }
        return max;
    }
}
```
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int count = 0;
        int temp = 0;
        Set<Character> set = new HashSet<Character>();
        if(s.length() == 0 ) return 0;
        if(s.length() == 1) return 1;
        for(int i = 0 ; i<s.length(); i++){
            if(temp>count){
                count = temp;
            }
            temp = 0;
            set.clear();
            for(int j=i ; j<s.length(); j++){
                if(set.contains(s.charAt(j))){
                 break;
                }
                temp++;
                set.add(s.charAt(j)); 

            }
        }
    return count;

    }
}
```