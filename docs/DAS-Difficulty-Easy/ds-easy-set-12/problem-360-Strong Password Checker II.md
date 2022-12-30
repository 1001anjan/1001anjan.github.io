---
layout: default
title: Strong Password Checker II
parent: Easy Set 12
grand_parent: DSA Easy Difficulty
nav_order: 20
permalink: /problem-360-Strong Password Checker II/
---
# Strong Password Checker II
A password is said to be strong if it satisfies all the following criteria:

* It has at least 8 characters.
* It contains at least one lowercase letter.
* It contains at least one uppercase letter.
* It contains at least one digit.
* It contains at least one special character. The special characters are the characters in the following string: "!@#$%^&*()-+".
* It does not contain 2 of the same character in adjacent positions (i.e., "aab" violates this condition, but "aba" does not).
Given a string password, return true if it is a strong password. Otherwise, return false.

##### Example 1:
```markdown
Input: password = "IloveLe3tcode!"
Output: true
Explanation: The password meets all the requirements. Therefore, we return true.
```
##### Example 2:
```markdown
Input: password = "Me+You--IsMyDream"
Output: false
Explanation: The password does not contain a digit and also contains 2 of the same character in adjacent positions. Therefore, we return false.
```
##### Example 3:
```markdown
Input: password = "1aB!"
Output: false
Explanation: The password does not meet the length requirement. Therefore, we return false.
```
##### Constraints:
* 1 <= password.length <= 100
* password consists of letters, digits, and special characters: "!@#$%^&*()-+".

### Solution:
```java
class Solution {
    public boolean strongPasswordCheckerII(String password) {
        if(password.length() < 8) return false;
        boolean lc = false, uc = false, d = false, sc = false;
        char prev = ' ';
        for(char crr : password.toCharArray()){
            if(prev == crr) return false;
            if(Character.isDigit(crr)){
                d = true;
            }else if(Character.isLetter(crr)){
                if(Character.isUpperCase(crr)){
                    uc= true;
                }else{
                    lc = true;
                }
            }else{
                sc = true;
            }
            prev = crr;
        }
        return lc && uc && d && sc;
    }
}
```