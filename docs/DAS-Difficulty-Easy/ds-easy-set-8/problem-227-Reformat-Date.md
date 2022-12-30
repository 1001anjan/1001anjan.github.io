---
layout: default
title: Reformat Date
parent: Easy Set 8
grand_parent: DSA Easy Difficulty
nav_order: 7
permalink: /problem-227-Reformat-Date/
---
# Reformat Date
Given a date string in the form Day Month Year, where:

* Day is in the set {"1st", "2nd", "3rd", "4th", ..., "30th", "31st"}.
* Month is in the set {"Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"}.
* Year is in the range [1900, 2100].

Convert the date string to the format YYYY-MM-DD, where:

* YYYY denotes the 4 digit year.
* MM denotes the 2 digit month.
* DD denotes the 2 digit day.

##### Example 1:
```markdown
Input: date = "20th Oct 2052"
Output: "2052-10-20"
```
##### Example 2:
```markdown
Input: date = "6th Jun 1933"
Output: "1933-06-06"
```
##### Example 3:
```markdown
Input: date = "26th May 1960"
Output: "1960-05-26"
```
##### Constraints:
* The given dates are guaranteed to be valid, so no error handling is necessary.

### Solution:
```java
class Solution {
    public String reformatDate(String date) {
        String[] strs = date.split(" ");
        StringBuilder sb = new StringBuilder();
        return sb.append(strs[2]).append("-").append(getFormatedMonth(strs[1])).append("-")
            .append(getFormatedDate(strs[0].substring(0,strs[0].length() - 2))).toString();
    }
    
    public String getFormatedMonth(String str){
        switch(str){
            case "Jan": return "01";
            case "Feb": return "02";
            case "Mar": return "03";
            case "Apr": return "04";
            case "May": return "05";
            case "Jun": return "06";
            case "Jul": return "07";
            case "Aug": return "08";
            case "Sep": return "09";
            case "Oct": return "10";
            case "Nov": return "11";
            case "Dec": return "12";
            case default: return "-1";
        }
        
    }
    public String getFormatedDate(String str){
        if(str.length() == 1) return "0".concat(str);
        return str;
    }
}
```