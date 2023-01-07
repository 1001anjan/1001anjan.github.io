---
layout: default
title: Interleaving String
parent: Medium Set 4
grand_parent: DSA Medium Difficulty
nav_order: 2
permalink: /problem-152-Interleaving String/
---
# Interleaving String
Given strings s1, s2, and s3, find whether s3 is formed by an interleaving of s1 and s2.

An interleaving of two strings s and t is a configuration where s and t are divided into n and m substrings respectively, such that:

* s = s1 + s2 + ... + sn
* t = t1 + t2 + ... + tm
* |n - m| <= 1
* The interleaving is s1 + t1 + s2 + t2 + s3 + t3 + ... or t1 + s1 + t2 + s2 + t3 + s3 + ...

Note: a + b is the concatenation of strings a and b.

##### Example 1:
![](../../assets/images/ds/interleave.jpeg)
```markdown
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
Output: true
Explanation: One way to obtain s3 is:
Split s1 into s1 = "aa" + "bc" + "c", and s2 into s2 = "dbbc" + "a".
Interleaving the two splits, we get "aa" + "dbbc" + "bc" + "a" + "c" = "aadbbcbcac".
Since s3 can be obtained by interleaving s1 and s2, we return true.
```
##### Example 2:
```markdown
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbaccc"
Output: false
Explanation: Notice how it is impossible to interleave s2 with any other string to obtain s3.
```
##### Example 3:
```markdown
Input: s1 = "", s2 = "", s3 = ""
Output: true
```
##### Constraints:
* 0 <= s1.length, s2.length <= 100
* 0 <= s3.length <= 200
* s1, s2, and s3 consist of lowercase English letters.

Follow up: Could you solve it using only O(s2.length) additional memory space?

### Solution:
###### Recursion with memoization
```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        int n1 = s1.length(), n2 = s2.length(), n3 = s3.length();
        // cheacking the length
        if(n1 + n2 != n3) return false;
        return dfsCheck(s1, s2, s3, n1, n2, n3, 0, 0, 0, new HashMap<>());
    }

    public boolean dfsCheck(String s1, String s2, String s3, int n1, int n2, int n3, 
        int p1, int p2, int p3, Map<String, Boolean> map){

        if(p3 == n3) return true;
        String key = p1+"-"+p2+"-"+p3;
        if(map.containsKey(key)) return map.get(key);

        // if p1 reached to the end
        if(p1 == n1){
            Boolean s =  s2.charAt(p2) == s3.charAt(p3) ? dfsCheck(s1, s2, s3, n1, n2, n3, p1, p2 + 1, p3 + 1, map) : false;
            map.put(key, s);
            return map.get(key);
        }
        
        if(p2 == n2){
            Boolean s =  s1.charAt(p1) == s3.charAt(p3) ? dfsCheck(s1, s2, s3, n1, n2, n3, p1 + 1, p2, p3 + 1, map) : false;
            map.put(key, s);
            return map.get(key);
        }
        Boolean f1 = s2.charAt(p2) == s3.charAt(p3) ? dfsCheck(s1, s2, s3, n1, n2, n3, p1, p2 + 1, p3 + 1, map) : false;
        Boolean f2 =  s1.charAt(p1) == s3.charAt(p3) ? dfsCheck(s1, s2, s3, n1, n2, n3, p1 + 1, p2, p3 + 1, map) : false;
        Boolean f = f1 || f2;
        map.put(key, f);
        return map.get(key);  

    }
}
```
##### Improvement:
```java
//1ms
class Solution {
    private boolean[][] invalid;
    private char[] c1;
    private char[] c2;
    private char[] c3;
    
    public boolean isInterleave(String s1, String s2, String s3) {
        c1 = s1.toCharArray();
        c2 = s2.toCharArray();
        c3 = s3.toCharArray();
        
        int m = s1.length(),n=s2.length();
        
        if(m + n != c3.length)
            return false;
        
        invalid = new boolean[m+1][n+1];
        
        return dfs(0,0,0);
    }
    
    public boolean dfs(int i, int j, int k){
        if(invalid[i][j])
            return false;
        
        if(k == c3.length)
            return true;
        
        boolean valid = 
            i < c1.length && c1[i] == c3[k] && dfs(i + 1,j,k + 1) || 
            j < c2.length && c2[j] == c3[k] && dfs(i,j + 1,k + 1);
        
        if(!valid)
            invalid[i][j] = true;
        
        return valid;
    }
}
```
###### Using 2D Dynamic Programming
```java
class Solution {
    
    public boolean isInterleave(String s1, String s2, String s3) {
        int n1 = s1.length(), n2 = s2.length(), n3 = s3.length();

        char[] c1 = s1.toCharArray();
        char[] c2 = s2.toCharArray();
        char[] c3 = s3.toCharArray();

        if(n1 + n2 != n3) return false;

        boolean[][] dp = new boolean[n1 + 1][n2 + 1];

        for(int i = 0; i <= n1; i++){
            for(int j = 0; j <= n2; j++){
                if(i == 0 && j == 0){
                    dp[i][j] = true;
                }else if(i == 0){
                    dp[i][j] = dp[i][j - 1] && c2[j - 1] == c3[i + j - 1];
                }else if(j == 0){
                    dp[i][j] = dp[i - 1][j] && c1[i - 1] == c3[i + j - 1];
                }else{
                    dp[i][j] = (c1[i - 1] == c3[i + j - 1] && dp[i - 1][j]) || (c2[j - 1] == c3[i + j - 1] && dp[i][j - 1]);
                }
            }
        }

        return dp[n1][n2];
    }
}
```
##### Using 1D Dynamic Programming
```java
class Solution {
    
    public boolean isInterleave(String s1, String s2, String s3) {
        int n1 = s1.length(), n2 = s2.length(), n3 = s3.length();

        char[] c1 = s1.toCharArray();
        char[] c2 = s2.toCharArray();
        char[] c3 = s3.toCharArray();

        if(n1 + n2 != n3) return false;

        boolean[] dp = new boolean[n2 + 1];

        for(int i = 0; i <= n1; i++){
            for(int j = 0; j <= n2; j++){
                if(i == 0 && j == 0){
                    dp[j] = true;
                }else if(i == 0){
                    dp[j] = dp[j - 1] && c2[j - 1] == c3[i + j - 1];
                }else if(j == 0){
                    dp[j] = dp[j] && c1[i - 1] == c3[i + j - 1];
                }else{
                    dp[j] = (c1[i - 1] == c3[i + j - 1] && dp[j]) || (c2[j - 1] == c3[i + j - 1] && dp[j - 1]);
                }
            }
        }

        return dp[n2];
    }
}
```
