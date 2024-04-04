---
layout: default
title: Longest Palindrome
parent: Easy Set 3
grand_parent: DSA Easy
nav_order: 12
permalink: /problem-75-Longest-Palindrome/
---
# Longest Palindrome

Given a string s which consists of lowercase or uppercase letters, return the length of the longest palindrome that can be built with those letters.

Letters are case sensitive, for example, "Aa" is not considered a palindrome here.

##### Example 1:
```markdown
Input: s = "abccccdd"
Output: 7
Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.
```
##### Example 2:
```markdown
Input: s = "a"
Output: 1
```
##### Example 3:
```markdown
Input: s = "bb"
Output: 2
```
##### Constraints:
* 1 <= s.length <= 2000
* s consists of lowercase and/or uppercase English letters only.

### Solution
```java
class Solution {
    public int longestPalindrome(String s) {
        Map<Character, Integer> m = new HashMap<Character,Integer>();
        for(int i = 0; i<s.length(); i++){
            m.put(s.charAt(i), m.getOrDefault(s.charAt(i),0)+1);
        }
        int a = 0;
        for(int i : m.values()){
            if(i%2 == 0){
                a = a + i;
            }else if(i>1){
                a += i - 1;
            }
        }
        if(s.length() > a) return a+1;
        return a;
    }
}
```
###### Faster approach
```java
class Solution {
    public int longestPalindrome(String s) {
        int[] count = new int[128];
        for (char c: s.toCharArray())
            count[c]++;

        int ans = 0;
        for (int v: count) {
            ans += v / 2 * 2;
            if (ans % 2 == 0 && v % 2 == 1)
                ans++;
        }
        return ans;
    }
}
```