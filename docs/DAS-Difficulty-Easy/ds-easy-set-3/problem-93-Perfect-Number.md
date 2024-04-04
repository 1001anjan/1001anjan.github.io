---
layout: default
title: Perfect Number
parent: Easy Set 3
grand_parent: DSA Easy
nav_order: 30
permalink: /problem-93-Perfect-Number/
---

# Perfect Number

A perfect number is a positive integer that is equal to the sum of its positive divisors, excluding the number itself. A divisor of an integer x is an integer that can divide x evenly.

Given an integer n, return true if n is a perfect number, otherwise return false.

##### Example 1:
```markdown
Input: num = 28
Output: true
Explanation: 28 = 1 + 2 + 4 + 7 + 14
1, 2, 4, 7, and 14 are all divisors of 28.
```

##### Example 2:
```markdown
Input: num = 7
Output: false
```
##### Constraints:
* 1 <= num <= 108

##### Solution:
```java
class Solution {
    public boolean checkPerfectNumber(int num) {
        int sum = 0;
        for(int i = 1; i<=num/2; i++){
            if(num%i == 0) sum += i;
            if(sum>num) return false;
        }
        if(sum == num) return true;
        
        return false;
    }
}
```
https://leetcode.com/problems/perfect-number/solution/
```java
class Solution {
    
    public boolean checkPerfectNumber(int num) {
        if (num <= 0) {
            return false;
        }
        int sum = 0;
        for (int i = 1; i * i <= num; i++) {
            if (num % i == 0) {
                sum += i;
                if (i * i != num) {
                    sum += num / i;
                }

            }
        }
        return sum - num == num;
    }
}

```