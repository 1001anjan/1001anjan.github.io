---
layout: default
title: Integer to Roman
parent: Medium Set 1
grand_parent: DSA Medium
nav_order: 8
permalink: /problem-8-Integer to Roman/
---
# Integer to Roman
Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.
```markdown
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```
For example, 2 is written as II in Roman numeral, just two one's added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

* I can be placed before V (5) and X (10) to make 4 and 9.
* X can be placed before L (50) and C (100) to make 40 and 90.
* C can be placed before D (500) and M (1000) to make 400 and 900.
Given an integer, convert it to a roman numeral.

##### Example 1:
```markdown
Input: num = 3
Output: "III"
Explanation: 3 is represented as 3 ones.
```
##### Example 2:
```markdown
Input: num = 58
Output: "LVIII"
Explanation: L = 50, V = 5, III = 3.
```
##### Example 3:
```markdown
Input: num = 1994
Output: "MCMXCIV"
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```
##### Constraints:
* 1 <= num <= 3999

### Solution:
```java
class Solution {
    public String intToRoman(int num) {
        StringBuilder sb = new StringBuilder();
        // Comparator for sotring decending order
        TreeMap<Integer, String> tm = new TreeMap<>((a,b)->(b - a));
        tm.put(1000,"M");
        tm.put(900,"CM");
        tm.put(500,"D");
        tm.put(400,"CD");
        tm.put(100,"C");
        tm.put(90,"XC");
        tm.put(50,"L");
        tm.put(40,"XL");
        tm.put(10,"X");
        tm.put(9,"IX");
        tm.put(5,"V");
        tm.put(4,"IV");
        tm.put(1,"I");

        for(Map.Entry<Integer,String> entry : tm.entrySet()){
            int key = entry.getKey();
            while(num >= key){
                sb.append(entry.getValue());
                num -= key;
            }
        }
        return sb.toString();
    }
}
```

```java
class Solution {
    
    public static String intToRoman(int num) {
        String M[] = {"", "M", "MM", "MMM"};
        String C[] = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
        String X[] = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
        String I[] = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
        return new StringBuilder()
        .append(M[num/1000])
        .append(C[(num%1000)/100])
        .append(X[(num%100)/10])
        .append(I[num%10]).toString();
    }
}
```