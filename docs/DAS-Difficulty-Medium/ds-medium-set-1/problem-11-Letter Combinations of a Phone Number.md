---
layout: default
title: Letter Combinations of a Phone Number
parent: Medium Set 1
grand_parent: DSA Medium
nav_order: 11
permalink: /problem-11-Letter Combinations of a Phone Number/
---
# Letter Combinations of a Phone Number
Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![](../../assets/images/ds/1200px-telephone-keypad2svg.png)

##### Example 1:
```markdown
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```
##### Example 2:
```markdown
Input: digits = ""
Output: []
```
##### Example 3:
```markdown
Input: digits = "2"
Output: ["a","b","c"]
```
##### Constraints:
* 0 <= digits.length <= 4
* digits[i] is a digit in the range ['2', '9'].

### Solution:
```java
class Solution {
    String[] mp = {"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
    public List<String> letterCombinations(String digits) {
        int n = digits.length();
        if(n == 0) return new ArrayList<String>();
        List<String> result = new ArrayList<>();
        if(n == 1){
            for(char ch : mp[Character.getNumericValue(digits.charAt(0))].toCharArray()){
                result.add(String.valueOf(ch));
            }
            return result;
        }

        List<String> ans = letterCombinations(digits.substring(1,n));
        for(char ch : mp[Character.getNumericValue(digits.charAt(0))].toCharArray()){
            for(String s : ans){
                result.add(ch+s);
            }
        }
        return result;
    }
}
```