---
layout: default
title: Three Divisors
parent: Easy Set 10
grand_parent: DSA Easy
nav_order: 20
permalink: /problem-300-Three-Divisors/
---
# Three Divisors
Given an integer n, return true if n has exactly three positive divisors. Otherwise, return false.

An integer m is a divisor of n if there exists an integer k such that n = k * m.

##### Example 1:
```markdown
Input: n = 2
Output: false
Explantion: 2 has only two divisors: 1 and 2.
```
##### Example 2:
```markdown
Input: n = 4
Output: true
Explantion: 4 has three divisors: 1, 2, and 4.
```
##### Constraints:
* 1 <= n <= 10^4

### Solution:
```java
class Solution {
    public boolean isThree(int n) {
        int c = 0;
        for(int i = 2; i <= n / 2; i++){
            if(n % i == 0){
                c++;
                if(c > 1) return false;
            }
        }
        return c == 1;
    }
}
```