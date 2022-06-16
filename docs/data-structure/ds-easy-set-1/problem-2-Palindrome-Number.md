---
layout: default
title: Palindrome Number
parent: Data Structure Easy Set 1
grand_parent: Data Structure
nav_order: 2
---

# 2. Palindrome Number
{: .no_toc }

Given an integer x, return true if x is palindrome integer.

An integer is a palindrome when it reads the same backward as forward.

For example, 121 is a palindrome while 123 is not.


### Example 1:
```markdown
Input: x = 121
Output: true
Explanation: 121 reads as 121 from left to right and from right to left.
```

### Example 2:
```markdown
Input: x = -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```
### Example 3:
```markdown
Input: x = 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

### Constraints:
```markdown
-231 <= x <= 231 - 1
```
### Solution
```java
class Solution {
    public boolean isPalindrome(int x) {
        if(x < 0) return false;
        int rev = 0;
        int original = x;
        while(x > 0){
            rev = rev*10 + x%10;
            x = x/10;
        }
        return rev == original? true : false;
    }
}
```
### Complexity Analysis:

* Time complexity : O(log10(n)). We divided the input by 10 for every iteration, so the time complexity is O(log10(n))

* Space complexity : O(1)O(1).