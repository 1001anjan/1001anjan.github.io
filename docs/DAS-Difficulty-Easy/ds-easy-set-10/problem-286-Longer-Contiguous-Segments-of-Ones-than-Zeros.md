---
layout: default
title: Longer Contiguous Segments of Ones than Zeros
parent: Easy Set 10
grand_parent: DSA Easy Difficulty
nav_order: 6
permalink: /problem-286-Longer-Contiguous-Segments-of-Ones-than-Zeros/
---
# Longer Contiguous Segments of Ones than Zeros
Given a binary string s, return true if the longest contiguous segment of 1's is strictly longer than the longest contiguous segment of 0's in s, or return false otherwise.

* For example, in s = "110100010" the longest continuous segment of 1s has length 2, and the longest continuous segment of 0s has length 3.
Note that if there are no 0's, then the longest continuous segment of 0's is considered to have a length 0. The same applies if there is no 1's.

##### Example 1:
```markdown
Input: s = "1101"
Output: true
Explanation:
The longest contiguous segment of 1s has length 2: "1101"
The longest contiguous segment of 0s has length 1: "1101"
The segment of 1s is longer, so return true.
```
##### Example 2:
```markdown
Input: s = "111000"
Output: false
Explanation:
The longest contiguous segment of 1s has length 3: "111000"
The longest contiguous segment of 0s has length 3: "111000"
The segment of 1s is not longer, so return false.
```
##### Example 3:
```markdown
Input: s = "110100010"
Output: false
Explanation:
The longest contiguous segment of 1s has length 2: "110100010"
The longest contiguous segment of 0s has length 3: "110100010"
The segment of 1s is not longer, so return false.
```
##### Constraints:
* 1 <= s.length <= 100
* s[i] is either '0' or '1'.

### Solution:
```java
class Solution {
    public boolean checkZeroOnes(String s) {
        int n = s.length();
        if(n == 1) return s.charAt(0) == '1';
        return longestSegmentLen(s,'1') > longestSegmentLen(s,'0');
    }
    
    public int longestSegmentLen(String s, char ch){
        int max = 0;
        char prev = s.charAt(0);
        int crr = prev == ch? 1 : 0;
        
        for(int i = 1; i < s.length(); i++){
            char now = s.charAt(i);
            if(prev == ch && prev == now) crr++;
            else{
                max = Math.max(max,crr);
                crr = 1;
            }
            prev = now;
        }
        return Math.max(max,crr);
    }
}
```
#### Single pass
```java
class Solution {
    public boolean checkZeroOnes(String s) {
        int n = s.length();
        if(n == 1) return s.charAt(0) == '1';
        int zeros = 0, ones = 0, zMax = -1, oMax = -1;

        for (int i = 0; i < n - 1; i++) {
            if (s.charAt(i) == s.charAt(i+1)) {
                if (s.charAt(i) == '0') zeros++;
                else ones++;
            }
            else {
                zMax = Integer.max(zeros, zMax);
                oMax = Integer.max(ones, oMax);
                zeros = 0;
                ones = 0;
            }
        }
        zMax = Integer.max(zeros, zMax);
        oMax = Integer.max(ones, oMax);

        return oMax > zMax;
    }
}
```
