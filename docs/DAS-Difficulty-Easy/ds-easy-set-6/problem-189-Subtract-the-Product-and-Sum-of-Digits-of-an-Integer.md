---
layout: default
title: Subtract the Product and Sum of Digits of an Integer
parent: Easy Set 6
grand_parent: DSA Easy
nav_order: 29
permalink: /problem-189-Subtract-the-Product-and-Sum-of-Digits-of-an-Integer/
---
# Subtract the Product and Sum of Digits of an Integer
Given an integer number n, return the difference between the product of its digits and the sum of its digits.

##### Example 1:
```markdown
Input: n = 234
Output: 15
Explanation:
Product of digits = 2 * 3 * 4 = 24
Sum of digits = 2 + 3 + 4 = 9
Result = 24 - 9 = 15
```
##### Example 2:
```markdown
Input: n = 4421
Output: 21
Explanation:
Product of digits = 4 * 4 * 2 * 1 = 32
Sum of digits = 4 + 4 + 2 + 1 = 11
Result = 32 - 11 = 21
```
##### Constraints:
* 1 <= n <= 10^5

### Solution:

```java
class Solution {
    public int subtractProductAndSum(int n) {
        int p = 1;
        int s = 0;
        
        while(n>0){
            int d = n%10;
            p *= d;
            s += d;
            n = n/10;
        }
        return p - s;
    }
}
```