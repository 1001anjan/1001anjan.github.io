---
layout: default
title: Longest Palindromic Substring
parent: Medium Set 1
grand_parent: DSA Medium
nav_order: 4
permalink: /problem-4-Longest Palindromic Substring/
---
# Longest Palindromic Substring
Given a string s, return the longest palindromic substring in s.

##### Example 1:
```markdown
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
```
##### Example 2:
```markdown
Input: s = "cbbd"
Output: "bb"
```
##### Constraints:
* 1 <= s.length <= 1000
* s consist of only digits and English letters.

### Solution:
```java
class Solution {
    public String longestPalindrome(String s) {
        int n = s.length();
        int start = 0, end = 0;
        boolean[][] dp = new boolean[n][n];
        for(int len = 0; len < n; len++){
            for(int i = 0; len + i < n; i++){
                dp[i][i + len] = (s.charAt(i) == s.charAt(i + len)) 
                && (len < 2 || dp[i + 1][i + len -1]);
                if(dp[i][i + len] && len > (end - start)){
                    start = i;
                    end = i + len;
                }
            }
        }
        return s.substring(start, end + 1);
    }
}
```
##### Logic:
The dynamic programmic approach to this question is quite simple actually! For any given substring, we can confirm if it is a palindrome in O(1) time if:

The characters at the ends of the substring are the same.
If the inner substring is a palindrome.
Observe this relationship below:
![](../../assets/images/ds/861e5558-0a38-4d01-bc08-aeb135cb80bd_1655340599.097208.png)
##### Algorithm:
* Our outter loop will represent our length - 1, len.
* Our inner loop will represent our left pointer, i.
Therefore, our right pointer will be represented by i+len. This makes our logic a bit easier:

Our base cases are when len is 0 or 1 (i.e. when the length of the substring is of length 1 or 2). In these situations, DP won't work. Thankfully, all we need to check for is whether s.charAt(i) == s.charAt(i + len).
For len > 1, we would also need to check whether the inner substring is a palindrome as illustrated above. Therefore, we'll also check if dp[i+1][i+len-1] is true.
There are a few ways we could keep track of our longest substring. We could just assign a new substring whenever our current window length is greater than the current string's length. However, assigning a new substring on each update takes O(n) time at worst. Therefore, we'll just keep track of the indices of our longest substring using start and end and we'll only convert this into a substring at the end.