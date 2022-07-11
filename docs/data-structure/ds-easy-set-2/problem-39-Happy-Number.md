---
layout: default
title: Happy Number
parent: Data Structure Easy Set 2
grand_parent: Data Structure
nav_order: 8
permalink: /problem-39-Number-of-1-Bits/
---
# Happy Number

Write an algorithm to determine if a number n is happy.

A happy number is a number defined by the following process:

* Starting with any positive integer, replace the number by the sum of the squares of its digits.
* Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
* Those numbers for which this process ends in 1 are happy.
* Return true if n is a happy number, and false if not.

##### Example 1:
```markdown
Input: n = 19
Output: true
Explanation:
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```
##### Example 2:
```markdown
Input: n = 2
Output: false
```

##### Constraints:
* 1 <= n <= 231 - 1
### Solution
```java
class Solution {
    public boolean isHappy(int n) {
       
        while(n != 1 && n != 4){
           n = getNext(n);
       }
        return n==1;
    }
    
    public int getNext(int n){
        int sum = 0;
        int d;
        while(n>0){
            d = n%10;
            sum += d*d;
            n = n/10;
        }
        return sum;
    }
}
```
##### Approach : Detect Cycles with a HashSet
More details: https://leetcode.com/problems/happy-number/solution/
```java
class Solution {
    public boolean isHappy(int n) {
        Set<Integer> set = new HashSet<Integer>();
        int sum = 0;
        int d;
        while(n != 1){
            n = getDigitsSum(n);
            if(set.contains(n)) return false;
            set.add(n);
        }
        return true;
    }
    public int getDigitsSum(int n){
        int sum = 0;
        int d;
        while(n>0){
            d = n%10;
            sum += d*d;
            n = n/10;
        }
        return sum;
    }
}
```
