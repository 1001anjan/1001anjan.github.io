---
layout: default
title: Excel Sheet Column Title
parent: Easy Set 2
grand_parent: DSA Easy Difficulty
nav_order: 3
permalink: /problem-34-Excel-Sheet-Column-Title/
---
# Excel Sheet Column Title

Given an integer columnNumber, return its corresponding column title as it appears in an Excel sheet.

##### For example:
```markdown
A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28
...
```
##### Example 1:
```markdown
Input: columnNumber = 1
Output: "A"
```

##### Example 2:
```markdown
Input: columnNumber = 28
Output: "AB"
```
##### Example 3:
```markdown
Input: columnNumber = 701
Output: "ZY"
```
##### Constraints:
* 1 <= columnNumber <= 231 - 1

### Solution
```java
class Solution {
    public String convertToTitle(int columnNumber) {
        StringBuilder sb = new StringBuilder();
        int digit;
        while(columnNumber>0){
            digit = (columnNumber-1)%26;
            sb.append((char)((int)'A' + digit));
            columnNumber = (columnNumber-1)/26;
         }
        return sb.reverse().toString();
    }
}
```