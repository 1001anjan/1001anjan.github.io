---
layout: default
title: A Number After a Double Reversal
parent: Easy Set 11
grand_parent: DSA Easy
nav_order: 19
permalink: /problem-329-A Number After a Double Reversal/
---
# A Number After a Double Reversal
Reversing an integer means to reverse all its digits.

For example, reversing 2021 gives 1202. Reversing 12300 gives 321 as the leading zeros are not retained.
Given an integer num, reverse num to get reversed1, then reverse reversed1 to get reversed2. Return true if reversed2 equals num. Otherwise return false.

##### Example 1:
```markdown
Input: num = 526
Output: true
Explanation: Reverse num to get 625, then reverse 625 to get 526, which equals num.
```
##### Example 2:
```markdown
Input: num = 1800
Output: false
Explanation: Reverse num to get 81, then reverse 81 to get 18, which does not equal num.
```
##### Example 3:
```markdown
Input: num = 0
Output: true
Explanation: Reverse num to get 0, then reverse 0 to get 0, which equals num.
```
##### Constraints:
* 0 <= num <= 106

### Solution:
```java
class Solution {
    public boolean isSameAfterReversals(int num) {
        if(num == 0) return true;
        if(num % 10 == 0) return false;
        return true;
    }
}
```