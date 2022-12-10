---
layout: default
title: Count Integers With Even Digit Sum
parent: Data Structure Easy Set 11
grand_parent: Data Structure
nav_order: 30
permalink: /problem-340-Count Integers With Even Digit Sum/
---
# Count Integers With Even Digit Sum
Given a positive integer num, return the number of positive integers less than or equal to num whose digit sums are even.

The digit sum of a positive integer is the sum of all its digits.

##### Example 1:
```markdown
Input: num = 4
Output: 2
Explanation:
The only integers less than or equal to 4 whose digit sums are even are 2 and 4.   
```
##### Example 2:
```markdown
Input: num = 30
Output: 14
Explanation:
The 14 integers less than or equal to 30 whose digit sums are even are
2, 4, 6, 8, 11, 13, 15, 17, 19, 20, 22, 24, 26, and 28.
```
##### Constraints:
* 1 <= num <= 1000

### Solution:
```java
class Solution {
    public int countEven(int num) {
        int c = 0;
        for(int i = 2; i <= num; i++){
            if(digitSum(i) % 2 == 0) c++;
        }
        return c;
    }
    
    public int digitSum(int n){
        int sum = 0;
        while(n > 0){
            sum += n % 10;
            n = n / 10;
        }
        return sum;
    }
}
```
##### Improvement
```java
class Solution {
    public boolean sumOfDigits(int n){
        int sum = 0;
        while(n != 0){
            sum += (n % 10);
            n = n / 10;
        }
        return sum %2 == 0 ? true : false;
    }
    public int countEven(int num) {
        int c = 0;
        for(int i = 2;i <= num; i++){
            if(i < 10 && i %2 == 0)
                c++;
            else if(sumOfDigits(i) == true)
                c++;
        }
        return c;
    }
}
```