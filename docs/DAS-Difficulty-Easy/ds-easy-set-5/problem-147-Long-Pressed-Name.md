---
layout: default
title: Long Pressed Name
parent: Easy Set 5
grand_parent: DSA Easy
nav_order: 17
permalink: /problem-147-Long-Pressed-Name/
---
# Long Pressed Name

Your friend is typing his name into a keyboard. Sometimes, when typing a character c, the key might get long pressed, and the character will be typed 1 or more times.

You examine the typed characters of the keyboard. Return True if it is possible that it was your friends name, with some characters (possibly none) being long pressed.

##### Example 1:
```markdown
Input: name = "alex", typed = "aaleex"
Output: true
Explanation: 'a' and 'e' in 'alex' were long pressed.
```
##### Example 2:
```markdown
Input: name = "saeed", typed = "ssaaedd"
Output: false
Explanation: 'e' must have been pressed twice, but it was not in the typed output.
```
##### Constraints:
* 1 <= name.length, typed.length <= 1000
* name and typed consist of only lowercase English letters.

### Solution:
```java
class Solution {
    public boolean isLongPressedName(String name, String typed) {
        int i = 0;
        int j = 0;
        while(i<name.length() && j<typed.length()){
            System.out.println("i"+i+" j: "+j);
            if(name.charAt(i) == typed.charAt(j)){
                i++;
                j++;
            }else{
                if(j == 0) break;
                if(typed.charAt(j-1) != typed.charAt(j)) break;
                while(j<typed.length() && typed.charAt(j-1) == typed.charAt(j)) j++;
            }
        }
        while(j != 0 && j<typed.length() && typed.charAt(j-1) == typed.charAt(j)) j++;
        return i == name.length() && j == typed.length();
    }
}
```