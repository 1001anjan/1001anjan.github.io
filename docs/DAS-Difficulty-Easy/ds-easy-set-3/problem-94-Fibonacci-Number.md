---
layout: default
title: Fibonacci Number
parent: Easy Set 3
grand_parent: DSA Easy
nav_order: 31
permalink: /problem-94-Fibonacci-Number/
---
# Fibonacci Number

The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is,
```markdown
F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1.
```
Given n, calculate F(n).

##### Example 1:
```markdown
Input: n = 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.
```
##### Example 2:
```markdown
Input: n = 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.
```
#### Example 3:
```markdown
Input: n = 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
```
##### Constraints:
* 0 <= n <= 30

### Solution
```java
class Solution {
    public int fib(int n) {
        if(n == 0) return 0;
        if(n == 1) return 1;
        return fib(n-1) + fib(n-2);
    }
}
```
```java
class Solution {
    Map<Integer,Integer> map = new HashMap<>();
    public int fib(int n) {
        if(map.containsKey(n)) return map.get(n); 
        if(n == 0) return 0;
        if(n == 1) return 1;
        map.put(n,fib(n-1) + fib(n-2));
        return map.get(n);
    }
}
```