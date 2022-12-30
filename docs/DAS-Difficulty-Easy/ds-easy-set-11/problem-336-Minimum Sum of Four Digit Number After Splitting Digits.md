---
layout: default
title: Minimum Sum of Four Digit Number After Splitting Digits
parent: Easy Set 11
grand_parent: DSA Easy Difficulty
nav_order: 26
permalink: /problem-336-Minimum Sum of Four Digit Number After Splitting Digits/
---
# Minimum Sum of Four Digit Number After Splitting Digits
You are given a positive integer num consisting of exactly four digits. Split num into two new integers new1 and new2 by using the digits found in num. Leading zeros are allowed in new1 and new2, and all the digits found in num must be used.

* For example, given num = 2932, you have the following digits: two 2's, one 9 and one 3. Some of the possible pairs [new1, new2] are [22, 93], [23, 92], [223, 9] and [2, 329].
Return the minimum possible sum of new1 and new2.

##### Example 1:
```markdown
Input: num = 2932
Output: 52
Explanation: Some possible pairs [new1, new2] are [29, 23], [223, 9], etc.
The minimum sum can be obtained by the pair [29, 23]: 29 + 23 = 52.
```
##### Example 2:
```markdown
Input: num = 4009
Output: 13
Explanation: Some possible pairs [new1, new2] are [0, 49], [490, 0], etc.
The minimum sum can be obtained by the pair [4, 9]: 4 + 9 = 13.
```
##### Constraints:
* 1000 <= num <= 9999

### Solution:
```java
class Solution {
    public int minimumSum(int num) {
        int[] d = new int[4];
        int i = 0;
        while(num > 0){
            d[i++] = num % 10;
            num = num / 10;
        }
        Arrays.sort(d);
        int d1 = d[0] * 10 + d[2];
        int d2 = d[1] * 10 + d[3];
        return d1 + d2;
    }
}
```