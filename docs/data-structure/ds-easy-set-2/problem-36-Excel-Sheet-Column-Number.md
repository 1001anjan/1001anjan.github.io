---
layout: default
title: Excel Sheet Column Number
parent: Data Structure Easy Set 2
grand_parent: Data Structure
nav_order: 5
permalink: /problem-36-Excel-Sheet-Column-Number/
---
# Excel Sheet Column Number

Given a string columnTitle that represents the column title as appears in an Excel sheet, return its corresponding column number.

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
Input: columnTitle = "A"
Output: 1
```
##### Example 2:
```markdown
Input: columnTitle = "AB"
Output: 28
```
##### Example 3:
````markdown
Input: columnTitle = "ZY"
Output: 701
````
### Constraints:

* 1 <= columnTitle.length <= 7
* columnTitle consists only of uppercase English letters.
* columnTitle is in the range ["A", "FXSHRXW"].

### Solution
```java
class Solution {
    public int titleToNumber(String columnTitle) {
        int ans = 0;
        for(int i=0; i<=columnTitle.length() -1; i++){
           ans = 26*ans + columnTitle.charAt(i) - 'A' +1;
        }
        return ans;
    }
}
```