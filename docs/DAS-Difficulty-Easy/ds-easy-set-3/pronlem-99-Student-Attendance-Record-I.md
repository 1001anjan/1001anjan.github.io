---
layout: default
title: Student Attendance Record I
parent: Easy Set 3
grand_parent: DSA Easy Difficulty
nav_order: 36
permalink: /problem-99-Student-Attendance-Record-I/
---
# Student Attendance Record I

You are given a string s representing an attendance record for a student where each character signifies whether the student was absent, late, or present on that day. The record only contains the following three characters:

* 'A': Absent.
* 'L': Late.
* 'P': Present.
The student is eligible for an attendance award if they meet both of the following criteria:

* The student was absent ('A') for strictly fewer than 2 days total.
* The student was never late ('L') for 3 or more consecutive days.
* Return true if the student is eligible for an attendance award, or false otherwise.

##### Example 1:
```markdown
Input: s = "PPALLP"
Output: true
Explanation: The student has fewer than 2 absences and was never late 3 or more consecutive days.
```
###### Example 2:
```markdown
Input: s = "PPALLL"
Output: false
Explanation: The student was late 3 consecutive days in the last 3 days, so is not eligible for the award.
```
##### Constraints:
* 1 <= s.length <= 1000
* s[i] is either 'A', 'L', or 'P'.

### Solution:
```java
class Solution {
    public boolean checkRecord(String s) {
        int abs = 0;
        int late = 0;
        int i = 0;
        while(i<s.length()){
            char ch = s.charAt(i);
            if(ch == 'A') abs++;
            if(ch == 'L'){
                late++;
                i++;
                while(i<s.length()){
                    ch = s.charAt(i);
                    if(ch != 'L'){
                        i--;
                        break;
                    }else{
                        late++;
                        i++;
                    }
                }
                if(late>=3) return false;
                late = 0;
            }
            i++;
        }
        if(abs>=2 ) return false;
        return true;
    }
}
```