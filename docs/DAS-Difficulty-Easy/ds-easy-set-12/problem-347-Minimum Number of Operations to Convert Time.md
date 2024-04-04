---
layout: default
title: Minimum Number of Operations to Convert Time
parent: Easy Set 12
grand_parent: DSA Easy
nav_order: 7
permalink: /problem-347-Minimum Number of Operations to Convert Time/
---
# Minimum Number of Operations to Convert Time
You are given two strings current and correct representing two 24-hour times.

24-hour times are formatted as "HH:MM", where HH is between 00 and 23, and MM is between 00 and 59. The earliest 24-hour time is 00:00, and the latest is 23:59.

In one operation you can increase the time current by 1, 5, 15, or 60 minutes. You can perform this operation any number of times.

Return the minimum number of operations needed to convert current to correct.

##### Example 1:
```markdown
Input: current = "02:30", correct = "04:35"
Output: 3
Explanation:
We can convert current to correct in 3 operations as follows:
- Add 60 minutes to current. current becomes "03:30".
- Add 60 minutes to current. current becomes "04:30".
- Add 5 minutes to current. current becomes "04:35".
  It can be proven that it is not possible to convert current to correct in fewer than 3 operations.
```
##### Example 2:
```markdown
Input: current = "11:00", correct = "11:01"
Output: 1
Explanation: We only have to add one minute to current, so the minimum number of operations needed is 1.
```
##### Constraints:
* current and correct are in the format "HH:MM"
* current <= correct

### Solution:
```java
class Solution {
    public int convertTime(String current, String correct) {
        String[] cr = current.split(":");
        String[] co = correct.split(":");
        
        int minCurr = Integer.parseInt(cr[0]) * 60 + Integer.parseInt(cr[1]);
        int minCorr = Integer.parseInt(co[0]) * 60 + Integer.parseInt(co[1]);
        
        int minDiff = minCorr - minCurr;
        int op = 0;
        
        if(minDiff >= 60){
            int d = minDiff / 60;
            op += d;
            minDiff -= d * 60;
        }
        if(minDiff >= 15){
            int d = minDiff / 15;
            op += d;
            minDiff -= d * 15;
        }
        if(minDiff >= 5){
            int d = minDiff / 5;
            op += d;
            minDiff -= d * 5;
        }
        if(minDiff >= 1){
            op += minDiff;
        } 
        
        return op;
    }
}
```
##### Faster execution
```java
class Solution {
    public int  HHMMToMinutes(String s){
        return Integer.parseInt(s.substring(0,2))*60 + Integer.parseInt(s.substring(3,5)) ;
    }
    public int convertTime(String current, String correct) {
        int diff =  HHMMToMinutes(correct) -  HHMMToMinutes(current);
        int[] order = {60,15,5,1};
        int i = 0;
        int ops = 0;
        while(i < 4){
            ops += (diff / order[i]);
            diff %= order[i];
            i++;
        }
        return ops;
    }
}
```