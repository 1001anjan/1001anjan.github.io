---
layout: default
title: Count and Say
parent: Medium Set 1
grand_parent: DSA Medium Difficulty
nav_order: 19
permalink: /problem-19-Count and Say/
---
# Count and Say
The count-and-say sequence is a sequence of digit strings defined by the recursive formula:

* countAndSay(1) = "1"
* countAndSay(n) is the way you would "say" the digit string from countAndSay(n-1), which is then converted into a different digit string.

* To determine how you "say" a digit string, split it into the minimal number of substrings such that each substring contains exactly one unique digit. Then for each substring, say the number of digits, then say the digit. Finally, concatenate every said digit.

For example, the saying and conversion for digit string "3322251":
![](../../assets/images/ds/countandsay.jpeg)
Given a positive integer n, return the nth term of the count-and-say sequence.


##### Example 1:
```markdown
Input: n = 1
Output: "1"
Explanation: This is the base case.
```
##### Example 2:
```markdown
Input: n = 4
Output: "1211"
Explanation:
countAndSay(1) = "1"
countAndSay(2) = say "1" = one 1 = "11"
countAndSay(3) = say "11" = two 1's = "21"
countAndSay(4) = say "21" = one 2 + one 1 = "12" + "11" = "1211"
```
##### Constraints:
* 1 <= n <= 30

### Solution: 
```java
class Solution {
    public String countAndSay(int n) {
        if(n == 1) return "1";
        String dp = "1";
        for(int i = 2; i <= n; i++){
            dp = process(n, dp);
        }
        return dp;
    }

    public String process(int n, String s){
        int len = s.length();
        StringBuilder sb = new StringBuilder();
        for(int i = 0; i < len; ){
            int c = 0;
            int j = i;
            char ch = s.charAt(i);
            while(j < len){
                if(ch == s.charAt(j)){
                    j++;
                    c++;
                }else break;
            }
            i = j;
            sb.append(c).append(ch);
        }
        return sb.toString();
    }
}
```