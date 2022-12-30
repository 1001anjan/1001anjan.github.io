---
layout: default
title: Counting Bits
parent: Easy Set 2
grand_parent: DSA Easy Difficulty
nav_order: 29
permalink: /problem-60-Counting-Bits/
---
# Counting Bits

Given an integer n, return an array ans of length n + 1 such that for each i (0 <= i <= n), ans[i] is the number of 1's in the binary representation of i.

##### Example 1:
```markdown
Input: n = 2
Output: [0,1,1]
Explanation:
0 --> 0
1 --> 1
2 --> 10
```
##### Example 2:
```markdown
Input: n = 5
Output: [0,1,1,2,1,2]
Explanation:
0 --> 0
1 --> 1
2 --> 10
3 --> 11
4 --> 100
5 --> 101
```
##### Constraints:

* 0 <= n <= 105

### Solution
```java
class Solution {
    public int[] countBits(int n) {
        int[] ans = new int[n+1];
        ans[0] = 0;
        for(int i = 1; i <= n;i++){
            ans[i] = (i &1) + ans[i/2];
        }
        return ans;
    }
}
```

```java
class Solution {
    public int[] countBits(int n) {
        int[] ans = new int[n+1];
        for(int i=0; i<n+1; i++){
            ans[i] = count(Integer.toBinaryString(i));
        }
        return ans;
    }
    
    public int count(String s){
        int c = 0;
        for(int i=0; i<s.length(); i++)
            if(s.charAt(i) == '1') c++;
        
        return c;
    }
}
```
```java
class Solution {
    public int[] countBits(int n) {
        int[] ans = new int[n+1];
        int[] dp = new int[n+1];
        for(int i=0; i<=n; i++) dp[i] = -1;
        for (int i=0; i<=n; i++) {
            ans[i] = bits(i, dp);
        }
        
        return ans;
    }
    
    int bits(int n, int[] dp) {
        if (n == 0) return 0;
        if (n == 1) return 1;
        if (dp[n] != -1) return dp[n];
        int rem, quo;
        quo = n / 2;
        rem = n % 2;
        return dp[n] = (rem + bits(quo, dp));
    }
}
```