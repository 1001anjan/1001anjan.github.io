---
layout: default
title: Add Digits
parent: Data Structure Easy Set 2
grand_parent: Data Structure
nav_order: 22
permalink: /problem-53-Add-Digits/
---
# Add Digits

Given an integer num, repeatedly add all its digits until the result has only one digit, and return it.

##### Example 1:
```markdown
Input: num = 38
Output: 2
Explanation: The process is
38 --> 3 + 8 --> 11
11 --> 1 + 1 --> 2
Since 2 has only one digit, return it.
```
##### Example 2:
```markdown
Input: num = 0
Output: 0
```
##### Constraints:
* 0 <= num <= 231 - 1

### Solution
```java
class Solution {
    public int addDigits(int num) {
        if (num == 0) return 0;
        if (num % 9 == 0) return 9;
        return num % 9;
    }
}
```
```java
class Solution {
    public int addDigits(int num) {
        if(num<10) return num;
        while(num>9){
            num = getNext(num);
        }
        return num;
    }
    public int getNext(int n){
        int sum = 0;
        while(n>0){
            sum = sum + n%10;
            n = n/10;
        }
        return sum;
    }
}
```