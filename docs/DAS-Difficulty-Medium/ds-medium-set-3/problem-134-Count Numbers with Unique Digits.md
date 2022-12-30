---
layout: default
title: Count Numbers with Unique Digits
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 34
permalink: /problem-134-Count Numbers with Unique Digits/
---
# Count Numbers with Unique Digits
Given an integer n, return the count of all numbers with unique digits, x, where 0 <= x < 10n.

##### Example 1:
```markdown
Input: n = 2
Output: 91
Explanation: The answer should be the total numbers in the range of 0 ≤ x < 100, excluding 11,22,33,44,55,66,77,88,99
```
##### Example 2:
```markdown
Input: n = 0
Output: 1
```
##### Constraints:
* 0 <= n <= 8

### Solution:
```java
class Solution {
    public int countNumbersWithUniqueDigits(int n) {
        if(n == 0) return 1;
        int res = 10;
        int uniqueDigits = 9;
        int availableDigits = 9;
        while(n> 1 && availableDigits > 1){
            uniqueDigits = uniqueDigits * availableDigits;
            res += uniqueDigits;
            n --;
            availableDigits --;
        }
        return res;
    }
}
```