---
layout: default
title: Add Binary
parent: Easy Set 1
grand_parent: DSA Easy
nav_order: 14
permalink: /problem-14-add-binary/
---
# Add Binary

Given two binary strings a and b, return their sum as a binary string.

#### Example 1:
```markdown
Input: a = "11", b = "1"
Output: "100"
```
#### Example 2:
```markdown
Input: a = "1010", b = "1011"
Output: "10101"
```

### Constraints:
* 1 <= a.length, b.length <= 104
* a and b consist only of '0' or '1' characters.
* Each string does not contain leading zeros except for the zero itself.

### Solution
```java
class Solution {
    public String addBinary(String a, String b) {
        int reminder = 0;
        int i = a.length() - 1;
        int j = b.length() - 1;
        int p1, p2, sum;
        StringBuilder sb = new StringBuilder();
        while(i >= 0 || j >= 0 || reminder>0){
            p1 = i>=0? a.charAt(i)-48: 0;
            p2 = j>=0? b.charAt(j)-48: 0;
            sum = (p1+p2+reminder)%2;
            sb.append(sum);
            reminder = (p1+p2+reminder)/2;
            j--;
            i--;
        }
        return sb.reverse().toString();
    }
}
```