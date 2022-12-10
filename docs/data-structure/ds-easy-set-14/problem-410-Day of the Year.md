---
layout: default
title: Day of the Year
parent: Data Structure Easy Set 14
grand_parent: Data Structure
nav_order: 10
permalink: /problem-410-Day of the Year/
---
# Day of the Year
Given a string date representing a Gregorian calendar date formatted as YYYY-MM-DD, return the day number of the year.

##### Example 1:
```markdown
Input: date = "2019-01-09"
Output: 9
Explanation: Given date is the 9th day of the year in 2019.
```
##### Example 2:
```markdown
Input: date = "2019-02-10"
Output: 41
```
##### Constraints:
* date.length == 10
* date[4] == date[7] == '-', and all other date[i]'s are digits
* date represents a calendar date between Jan 1st, 1900 and Dec 31th, 2019.

### Solution:
```java
import java.time.LocalDate;

class Solution {
    public int dayOfYear(String date) {
        return LocalDate.parse(date).getDayOfYear();
    }
}
```

```java

class Solution {
   public int dayOfYear(String S) {
        String[] s = S.split("-");
        int year = Integer.parseInt(s[0]);
        int month = Integer.parseInt(s[1]);
        int date = Integer.parseInt(s[2]);
        boolean isLeap = checkYear(year);
        int noOfDays = 0;
        int[] days = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
        for (int i = 0; i < month - 1; i++) {
            if (isLeap && i == 1) {
                noOfDays += days[i] + 1;
                continue;
            }
            noOfDays += days[i];
        }
        return noOfDays + date;
    }
    boolean checkYear(int year) {
            if (year % 400 == 0)
                return true;
            if (year % 100 == 0)
                return false;
            if (year % 4 == 0)
                return true;
            return false;
        }
}
```