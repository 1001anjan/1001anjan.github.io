---
layout: default
title: N-th Tribonacci Number
parent: Data Structure Easy Set 6
grand_parent: Data Structure
nav_order: 16
permalink: /problem-176-N-th-Tribonacci-Number/
---
#  N-th Tribonacci Number
The Tribonacci sequence Tn is defined as follows:

T0 = 0, T1 = 1, T2 = 1, and Tn+3 = Tn + Tn+1 + Tn+2 for n >= 0.

Given n, return the value of Tn.

##### Example 1:
```markdown
Input: n = 4
Output: 4
Explanation:
T_3 = 0 + 1 + 1 = 2
T_4 = 1 + 1 + 2 = 4
```
##### Example 2:
```markdown
Input: n = 25
Output: 1389537
```
##### Constraints:
* 0 <= n <= 37
* The answer is guaranteed to fit within a 32-bit integer, ie. answer <= 2^31 - 1.

### Solution:
```java
class Solution {    
    public int tribonacci(int n) {
        int[] m = new int[38];
        return tribonacci(n,m);
    }
    
    public int tribonacci(int n, int[] m) {
        if(n == 0) return 0;
        if(n == 1) return 1;
        if(n == 2) return 1;
        int t1, t2, t3;
        
        if(m[n-1] == 0) 
            t1 = tribonacci(n-1, m);
        else
            t1 = m[n-1];
        if(m[n-2] == 0)
            t2 = tribonacci(n-2, m);
        else
            t2 = m[n-2];
        if(m[n-3] == 0)
            t3 = tribonacci(n-3, m);
        else
            t3 = m[n-3];
        
        m[n] = t1 + t2 + t3;
        return m[n];
    }
}
```