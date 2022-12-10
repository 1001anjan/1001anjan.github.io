---
layout: default
title: Convert Integer to the Sum of Two No-Zero Integers
parent: Data Structure Easy Set 7
grand_parent: Data Structure
nav_order: 7
permalink: /problem-197-Convert-Integer-to-the-Sum-of-Two-No-Zero Integers/
---
# Convert Integer to the Sum of Two No-Zero Integers

No-Zero integer is a positive integer that does not contain any 0 in its decimal representation.

Given an integer n, return a list of two integers [A, B] where:

A and B are No-Zero integers.
A + B = n
The test cases are generated so that there is at least one valid solution. If there are many valid solutions you can return any of them.

##### Example 1:
```markdown
Input: n = 2
Output: [1,1]
Explanation: A = 1, B = 1. A + B = n and both A and B do not contain any 0 in their decimal representation.
```
##### Example 2:
```markdown
Input: n = 11
Output: [2,9]
```
##### Constraints:
* 2 <= n <= 104

### Solution:

```java
class Solution {
    public int[] getNoZeroIntegers(int n) {
        int s = 1;
        int e = n-1;
        while(s<=e){
            if(checkNoZeroInteger(s) && checkNoZeroInteger(e))
                return new int[]{s,e};
            s++;
            e--;
        }
        throw null;
    }
    
    public boolean checkNoZeroInteger(int n){
        while(n>0){
            if(n%10 == 0) return false;
            n = n/10;
        }
        return true;
    }
}
```