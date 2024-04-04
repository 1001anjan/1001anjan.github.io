---
layout: default
title: Fraction to Recurring Decimal
parent: Medium Set 2
grand_parent: DSA Medium
nav_order: 35
permalink: /problem-85-Fraction to Recurring Decimal/
---
# Fraction to Recurring Decimal
Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

If the fractional part is repeating, enclose the repeating part in parentheses.

If multiple answers are possible, return any of them.

It is guaranteed that the length of the answer string is less than 104 for all the given inputs.

##### Example 1:
```markdown
Input: numerator = 1, denominator = 2
Output: "0.5"
```
##### Example 2:
```markdown
Input: numerator = 2, denominator = 1
Output: "2"
```
##### Example 3:
```markdown
Input: numerator = 4, denominator = 333
Output: "0.(012)"
```
##### Constraints:
* -2^31 <= numerator, denominator <= 2^31 - 1
* denominator != 0

### Solution:
```java
class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        if(denominator == 0) throw null;
        if(numerator == 0) return "0";
        StringBuilder sb = new StringBuilder();
        // checking sign of the result if one part is negetive 

        sb.append(((numerator > 0) ^ (denominator > 0)) ? "-" : "");

        long n = Math.abs((long) numerator);
        long d = Math.abs((long) denominator);

        sb.append(n/d);
        n %= d;
        if(n == 0) return sb.toString();
        sb.append(".");
        Map<Long, Integer> map = new HashMap<>();
        map.put(n, sb.length());

        while(n != 0){
            n *= 10;
            sb.append(n / d);
            n %= d;
            if(map.containsKey(n)){
                sb.insert(map.get(n),"(");
                sb.append(")");
                return sb.toString();
            }else{
                map.put(n, sb.length());
            }
        }
        return sb.toString();
    }
}
```