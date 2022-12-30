---
layout: default
title: Ugly Number II
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 13
permalink: /problem-113-Ugly Number II/
---
# Ugly Number II
An ugly number is a positive integer whose prime factors are limited to 2, 3, and 5.

Given an integer n, return the nth ugly number.

##### Example 1:
```markdown
Input: n = 10
Output: 12
Explanation: [1, 2, 3, 4, 5, 6, 8, 9, 10, 12] is the sequence of the first 10 ugly numbers.
```
##### Example 2:
```markdown
Input: n = 1
Output: 1
Explanation: 1 has no prime factors, therefore all of its prime factors are limited to 2, 3, and 5.
```
##### Constraints:
* 1 <= n <= 1690

### Solution:
##### Time Limit Exceeded
```java
class Solution {
    public int nthUglyNumber(int n) {
        if(n == 1) return 1;
        Set<Integer> set = new HashSet<>();
        set.add(1);
        
        int cnt = 1;
        int k = 2;
        while(cnt != n){
            if(k % 2 == 0 && set.contains(k / 2)){
                cnt++;
                set.add(k);
            }else if(k % 3 == 0 && set.contains(k / 3)){
                cnt++;
                set.add(k);
            }else if(k % 5 == 0 && set.contains(k / 5)){
                cnt++;
                set.add(k);
            }
            k++;
        }

        return k - 1;
    }
}
```

##### O(n) complexity
The ugly-number sequence is 1, 2, 3, 4, 5, 6, 8, 9, 10, 12, 15, …
because every number can only be divided by 2, 3, 5, one way to look at the sequence is to split the sequence to three groups as below:
```markdown
(1) 1×2, 2×2, 3×2, 4×2, 5×2, …
(2) 1×3, 2×3, 3×3, 4×3, 5×3, …
(3) 1×5, 2×5, 3×5, 4×5, 5×5, …
```
We can find that every subsequence is the ugly-sequence itself (1, 2, 3, 4, 5, …) multiply 2, 3, 5.

Then we use similar merge method as merge sort, to get every ugly number from the three subsequence.

Every step we choose the smallest one, and move one step after,including nums with same value.
```java
class Solution {
    public int nthUglyNumber(int n) {
       int[] ugly = new int[n];
       ugly[0] = 1;
       int factorOf2 = 2, factorOf3 = 3, factorOf5 = 5;
       int factor2Index = 0, factor3Index = 0, factor5Index = 0;
       for(int i = 1; i < n; i++){
           int min = Math.min(factorOf2, Math.min(factorOf3, factorOf5));
            ugly[i] = min;
           if(factorOf2 == min){
               factorOf2 = 2 * ugly[++factor2Index];
           }
           if(factorOf3 == min){
               factorOf3 = 3 * ugly[++factor3Index];
           }
           if(factorOf5 == min){
               factorOf5 = 5 * ugly[++factor5Index];
           }
       }
       return ugly[n - 1];
    }
}
```