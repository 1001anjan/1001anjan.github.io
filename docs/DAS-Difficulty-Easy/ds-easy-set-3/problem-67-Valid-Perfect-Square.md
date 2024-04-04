---
layout: default
title:  Valid Perfect Square
parent: Easy Set 3
grand_parent: DSA Easy
nav_order: 4
permalink: /problem-67-Valid-Perfect-Square/
---
# Valid Perfect Square

Given a positive integer num, write a function which returns True if num is a perfect square else False.

Follow up: Do not use any built-in library function such as sqrt.

##### Example 1:
```markdown
Input: num = 16
Output: true
```
##### Example 2:
```markdown
Input: num = 14
Output: false
```
##### Constraints:
* 1 <= num <= 2^31 - 1

### Solution
```java
class Solution {
    public boolean isPerfectSquare(int num) {
        int start = 0;
        int end = num;

        if(num == 1) return true;
    
        while (start <= end){
            long mid = start + (end - start)/2;
            if(mid * mid == num) return true;
            if(num > mid * mid) start = (int)mid + 1;
            if(num < mid * mid) end = (int)mid - 1;
        }
        return false;
    }
}
```