---
layout: default
title: Sum of Digits in Base K
parent: Easy Set 10
grand_parent: DSA Easy
nav_order: 1
permalink: /problem-281-Sum-of-Digits-in-Base-K/
---
# Sum of Digits in Base K
Given an integer n (in base 10) and a base k, return the sum of the digits of n after converting n from base 10 to base k.

After converting, each digit should be interpreted as a base 10 number, and the sum should be returned in base 10.

##### Example 1:
```markdown
Input: n = 34, k = 6
Output: 9
Explanation: 34 (base 10) expressed in base 6 is 54. 5 + 4 = 9.
```
##### Example 2:
```markdown
Input: n = 10, k = 10
Output: 1
Explanation: n is already in base 10. 1 + 0 = 1.
```
##### Constraints:
* 1 <= n <= 100
* 2 <= k <= 10

### Solution:
```java
class Solution {
    public int sumBase(int n, int k) {
        int sum = 0;
        while(n > 0){
            sum += n % k;
            n = n / k;
        }
        return sum;
    }
}
```