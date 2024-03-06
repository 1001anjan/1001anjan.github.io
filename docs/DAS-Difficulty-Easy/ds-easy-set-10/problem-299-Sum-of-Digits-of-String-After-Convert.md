---
layout: default
title: Sum of Digits of String After Convert
parent: Easy Set 10
grand_parent: DSA Easy
nav_order: 19
permalink: /problem-299-Sum of Digits of String After Convert/
---
# Sum of Digits of String After 
You are given a string s consisting of lowercase English letters, and an integer k.

First, convert s into an integer by replacing each letter with its position in the alphabet (i.e., replace 'a' with 1, 'b' with 2, ..., 'z' with 26). Then, transform the integer by replacing it with the sum of its digits. Repeat the transform operation k times in total.

For example, if s = "zbax" and k = 2, then the resulting integer would be 8 by the following operations:

* Convert: "zbax" ➝ "(26)(2)(1)(24)" ➝ "262124" ➝ 262124
* Transform #1: 262124 ➝ 2 + 6 + 2 + 1 + 2 + 4 ➝ 17
* Transform #2: 17 ➝ 1 + 7 ➝ 8
* Return the resulting integer after performing the operations described above.

##### Example 1:
```markdown
Input: s = "iiii", k = 1
Output: 36
Explanation: The operations are as follows:
- Convert: "iiii" ➝ "(9)(9)(9)(9)" ➝ "9999" ➝ 9999
- Transform #1: 9999 ➝ 9 + 9 + 9 + 9 ➝ 36
  Thus the resulting integer is 36.
```
##### Example 2:
```markdown
Input: s = "leetcode", k = 2
Output: 6
Explanation: The operations are as follows:
- Convert: "leetcode" ➝ "(12)(5)(5)(20)(3)(15)(4)(5)" ➝ "12552031545" ➝ 12552031545
- Transform #1: 12552031545 ➝ 1 + 2 + 5 + 5 + 2 + 0 + 3 + 1 + 5 + 4 + 5 ➝ 33
- Transform #2: 33 ➝ 3 + 3 ➝ 6
  Thus the resulting integer is 6.
  Example 3:

Input: s = "zbax", k = 2
Output: 8
```
##### Constraints:
* 1 <= s.length <= 100
* 1 <= k <= 10
* s consists of lowercase English letters.

### Solution:
```java
class Solution {
    public int getLucky(String s, int k) {
        StringBuilder sb1 = new StringBuilder();
        for(char c : s.toCharArray()) sb1.append(c - 96);
        int sum = 0;
        while(k >= 1){
            sum = 0;
            for(char c : sb1.toString().toCharArray()) sum += c - 48;
            sb1.setLength(0);
            sb1.append(sum);
            k--;
        }
        return sum;
    }
}
```

##### Improvement-->
```java
class Solution {
    public static int getLucky(String s, int k) {

        int totalAddedValue = toInteger(s);
        for(int roundCounter = 1; roundCounter < k; roundCounter++){

            totalAddedValue = addDigitsOfNumbers(totalAddedValue);

        }
        return totalAddedValue;
    }
    public static int toInteger(String s) {

        int integerValueOfString = 0;
        int valueAdde;
        for(int index = 0; index < s.length(); index++){

            integerValueOfString = (integerValueOfString + 
                                    addDigitsOfNumbers((int)(s.charAt(index) - 96)));

        }
        return integerValueOfString;
    }

    public static int addDigitsOfNumbers(int number) {

        int addedValue = 0;
        while (number != 0){
             addedValue = addedValue + (number % 10);
             number = number / 10;
        }
        return addedValue;
    }
}
```
