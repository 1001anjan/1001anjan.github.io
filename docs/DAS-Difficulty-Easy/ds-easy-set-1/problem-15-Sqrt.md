---
layout: default
title: Sqrt(x)
parent: Easy Set 1
grand_parent: DSA Easy Difficulty
nav_order: 15
permalink: /problem-15-sqrt/
---
# Sqrt(x)
Given a non-negative integer x, compute and return the square root of x.

Since the return type is an integer, the decimal digits are truncated, and only the integer part of the result is returned.

Note: You are not allowed to use any built-in exponent function or operator, such as pow(x, 0.5) or x ** 0.5.



#### Example 1:
```markdown
Input: x = 4
Output: 2
```
#### Example 2:
```markdown
Input: x = 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since the decimal part is truncated, 2 is returned.
```
### Constraints:
* 0 <= x <= 231 - 1

### Solution
```java
class Solution {
    public int mySqrt(int x) {
        if(x<2) return x;
        int start = 2;
        int end   = x/2;
        int mid = (start+end)/2;
        long res;
        while(start <= end){
            res = (long)mid*mid;
            if(res == x) return mid;
            if(res>x)
                end = mid - 1;
            else
                start = mid + 1;
            mid = (start+end)/2;
        }
        return mid;
    }
}
```