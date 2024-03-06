---
layout: default
title: Latest Time by Replacing Hidden Digits
parent: Easy Set 9
grand_parent: DSA Easy
nav_order: 12
permalink: /problem-262-Latest-Time-by-Replacing-Hidden-Digits/
---
# Latest Time by Replacing Hidden Digits
You are given a string time in the form of hh:mm, where some of the digits in the string are hidden (represented by ?).

The valid times are those inclusively between 00:00 and 23:59.

Return the latest valid time you can get from time by replacing the hidden digits.

##### Example 1:
```markdown
Input: time = "2?:?0"
Output: "23:50"
Explanation: The latest hour beginning with the digit '2' is 23 and the latest minute ending with the digit '0' is 50.
```
##### Example 2:
```markdown
Input: time = "0?:3?"
Output: "09:39"
```
##### Example 3:
```markdown
Input: time = "1?:22"
Output: "19:22"
```
##### Constraints:
* time is in the format hh:mm.
* It is guaranteed that you can produce a valid time from the given string.

### Solution:
```java
class Solution {
    public String maximumTime(String t) {
        char[] time = t.toCharArray();
        
        if(time[4]=='?'){
            time[4]='9';
        }
        if(time[3]=='?'){
            time[3]='5';
        }
        if(time[0]=='?'){
            if(time[1]=='1'||time[1]=='2'||time[1]=='3'||time[1]=='0'){
                time[0]='2';
            }
            else if(time[1]=='?'){
                time[0]='2';
            }else{
                time[0]='1';
            }
        }
        if(time[1]=='?'){
            if(time[0]=='0'){
                  time[1]='9';
            }
            else if(time[0]=='1'){
                 time[1]='9';
            }else if(time[0]=='2'){
                 time[1]='3';
            }
        }
        return new String(time);    
    }
}
```