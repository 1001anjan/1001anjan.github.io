---
layout: default
title: Factorial Trailing Zeroes
parent: Medium Set 2
grand_parent: DSA Medium
nav_order: 37
permalink: /problem-87-Factorial Trailing Zeroes/
---
# Factorial Trailing Zeroes
Given an integer n, return the number of trailing zeroes in n!.

Note that n! = n * (n - 1) * (n - 2) * ... * 3 * 2 * 1.

##### Example 1:
```markdown
Input: n = 3
Output: 0
Explanation: 3! = 6, no trailing zero.
```
##### Example 2:
```markdown
Input: n = 5
Output: 1
Explanation: 5! = 120, one trailing zero.
```
##### Example 3:
````markdown
Input: n = 0
Output: 0
````
##### Constraints:
* 0 <= n <= 10^4

### Solution:
0 is the product of 2 and 5. In n!, we need to know how many 2 and 5, and the number of zeros is the minimum of the number of 2 and the number of 5.

Since multiple of 2 is more than multiple of 5, the number of zeros is dominant by the number of 5.

Here we expand

2147483647!
```markdown
=2 * 3 * ...* 5 ... *10 ... 15* ... * 25 ... * 50 ... * 125 ... * 250...
=2 * 3 * ...* 5 ... * (5^1*2)...(5^1*3)...*(5^2*1)...*(5^2*2)...*(5^3*1)...*(5^3*2)... (Equation 1)
```
We just count the number of 5 in Equation 1.

Multiple of 5 provides one 5, multiple of 25 provides two 5 and so on.

Note the duplication: multiple of 25 is also multiple of 5, so multiple of 25 only provides one extra 5.

Here is the basic solution:

```markdown
return n/5 + n/25 + n/125 + n/625 + n/3125+...;
```
```java
class Solution {
    public int trailingZeroes(int n) {
        int count = 0;
        while(n > 0){
            count += n/5;
            n /= 5;
        }
        return count;
    }
}
```
