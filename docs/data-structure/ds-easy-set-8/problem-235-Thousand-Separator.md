---
layout: default
title: Thousand Separator
parent: Data Structure Easy Set 8
grand_parent: Data Structure
nav_order: 15
permalink: /problem-235-Thousand-Separator/
---
# Thousand Separator
Given an integer n, add a dot (".") as the thousands separator and return it in string format.

##### Example 1:
```markdown
Input: n = 987
Output: "987"
```
##### Example 2:
```markdown
Input: n = 1234
Output: "1.234"
```
##### Constraints:
* 0 <= n <= 231 - 1

### Solution:
```java
class Solution {
    public String thousandSeparator(int n) {
        if(n == 0) return "0";
        StringBuilder sb = new StringBuilder();
        int count = 0;
        while(n > 0){
            if(count == 3){
                count = 0;
                sb.append(".");
            }
            sb.append(n % 10);
            n = n/10;
            count++;
        }
        
        return sb.reverse().toString();
    }
}
```