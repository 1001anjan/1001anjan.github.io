---
layout: default
title: Number of Days Between Two Dates
parent: Easy Set 14
grand_parent: DSA Easy Difficulty
nav_order: 17
permalink: /problem-417-Number of Days Between Two Dates/
---
# Number of Days Between Two Dates
Write a program to count the number of days between two dates.

The two dates are given as strings, their format is YYYY-MM-DD as shown in the examples.

##### Example 1:
```markdown
Input: date1 = "2019-06-29", date2 = "2019-06-30"
Output: 1
```
##### Example 2:
```markdown
Input: date1 = "2020-01-15", date2 = "2019-12-31"
Output: 15
```
##### Constraints:
* The given dates are valid dates between the years 1971 and 2100.

### Solution: 

```java
class Solution {
    int dM[] = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
    public int daysBetweenDates(String date1, String date2) {
        String ds1[] = date1.split("-");
        String ds2[] = date2.split("-");
        
        int ddy1 = Integer.parseInt(ds1[0]);
        int ddm1 = Integer.parseInt(ds1[1]);
        int ddd1 = Integer.parseInt(ds1[2]);
        
        int ddy2 = Integer.parseInt(ds2[0]);
        int ddm2 = Integer.parseInt(ds2[1]);
        int ddd2 = Integer.parseInt(ds2[2]);
        
        int dy1, dy2, dm1, dm2, dd1, dd2;
        dy1 = ddy1;
        dm1 = ddm1;
        dd1 = ddd1;

        dy2 = ddy2;
        dm2 = ddm2;
        dd2 = ddd2;
        if(ddy1 > ddy2){
            dy1 = ddy2;
            dm1 = ddm2;
            dd1 = ddd2;
            
            dy2 = ddy1;
            dm2 = ddm1;
            dd2 = ddd1;
        }else if(ddy1 == ddy2 && ddm1 > ddm2){
            dy1 = ddy2;
            dm1 = ddm2;
            dd1 = ddd2;
            
            dy2 = ddy1;
            dm2 = ddm1;
            dd2 = ddd1;
        }else if(ddy1 == ddy2 && ddm1 == ddm2 && ddd1 > ddd2){
            dy1 = ddy2;
            dm1 = ddm2;
            dd1 = ddd2;
            
            dy2 = ddy1;
            dm2 = ddm1;
            dd2 = ddd1;
        }
        
        int count = 0;
        
        // cheacking is date1 and date2 if same year and same month
        if(dy1 == dy2 && dm1 == dm2){
            return dd2 - dd1;
        }
        // adding reaming day in the month
        count += dM[dm1] - dd1;
        if(dm1 == 2 && isLeapYear(dy1)){
            count++;
        }
        dm1++;
        // counting first year
        if(dy1 < dy2){
            while(dm1 <= 12){
                if(dm1 == 2 && isLeapYear(dy1)) count++;
                count += dM[dm1];
                dm1++;
            }
        }
        dy1++;
        // counting middle years
        while(dy1 < dy2){
            if(isLeapYear(dy1)) count++;
            count += 365;
            dy1++;
        }
        // countiing end year
        dm1 = 1;
        while(dy1 <= dy2 && dm1 < dm2){
            if(dm1 == 2 && isLeapYear(dy1)) count++;
            count += dM[dm1];
            dm1++;
        }
        // counting last month
        count += dd2;
        return count;
        
    }
    
    public boolean isLeapYear(int y){
        if(y % 400 == 0) return true;
        if(y % 100 == 0) return false;
        if(y % 4 == 0) return true;
        return false;
    }
}
```

