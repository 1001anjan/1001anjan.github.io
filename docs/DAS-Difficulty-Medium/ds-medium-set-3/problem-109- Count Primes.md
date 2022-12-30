---
layout: default
title: Count Primes
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 9
permalink: /problem-109-Count Primes/
---
# Count Primes
Given an integer n, return the number of prime numbers that are strictly less than n.

##### Example 1:
```markdown
Input: n = 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
```
##### Example 2:
```markdown
Input: n = 0
Output: 0
```
##### Example 3:
```markdown
Input: n = 1
Output: 0
```
##### Constraints:
* 0 <= n <= 5 * 10^6

### Solution:
```java
class Solution {
    public int countPrimes(int n) {
        boolean[] notPrime = new boolean[n];
        int count = 0;
        for(int i = 2; i < n; i++){
            if(notPrime[i] == false){
                count ++;
                for(int j = 2; (i * j) < n ; j++){
                    notPrime[i * j] = true;
                }
            }
        }
        return count;
    }
}
```