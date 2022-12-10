---
layout: default
title: Maximum 69 Number
parent: Data Structure Easy Set 7
grand_parent: Data Structure
nav_order: 8
permalink: /problem-198-Maximum-69-Number/
---
# Maximum 69 Number
You are given a positive integer num consisting only of digits 6 and 9.

Return the maximum number you can get by changing at most one digit (6 becomes 9, and 9 becomes 6).

##### Example 1:
```markdown
Input: num = 9669
Output: 9969
Explanation:
Changing the first digit results in 6669.
Changing the second digit results in 9969.
Changing the third digit results in 9699.
Changing the fourth digit results in 9666.
The maximum number is 9969.
```
##### Example 2:
```markdown
Input: num = 9996
Output: 9999
Explanation: Changing the last digit 6 to 9 results in the maximum number.
```
##### Example 3:
```markdown
Input: num = 9999
Output: 9999
Explanation: It is better not to apply any change.
```
##### Constraints:
* 1 <= num <= 104
* num consists of only 6 and 9 digits.

### Solution:
```java
class Solution {
    public int maximum69Number (int num) {
        String s = String.valueOf(num);
        StringBuilder sb = new StringBuilder();
        boolean f = true;
        for(char c : s.toCharArray()){
            if(c == '6' && f){
                sb.append("9");
                f = false;
            }
            else
                sb.append(String.valueOf(c));
        }
        return Integer.parseInt(sb.toString());
    }
}
```