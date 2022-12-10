---
layout: default
title: Path Crossing
parent: Data Structure Easy Set 8
grand_parent: Data Structure
nav_order: 5
permalink: /problem-225-Path-Crossing/
---
# Path Crossing
Given a string path, where path[i] = 'N', 'S', 'E' or 'W', each representing moving one unit north, south, east, or west, respectively. You start at the origin (0, 0) on a 2D plane and walk on the path specified by path.

Return true if the path crosses itself at any point, that is, if at any time you are on a location you have previously visited. Return false otherwise.

##### Example 1:
![](../../assets/images/ds/screen-shot-2020-06-10-at-123929-pm.png![img.png](img.png))
```markdown
Input: path = "NES"
Output: false
Explanation: Notice that the path doesn't cross any point more than once.
```
##### Example 2:
![](../../assets/images/ds/screen-shot-2020-06-10-at-123843-pm.png)
```markdown
Input: path = "NESWW"
Output: true
Explanation: Notice that the path visits the origin twice.
```
##### Constraints:
* 1 <= path.length <= 104
* path[i] is either 'N', 'S', 'E', or 'W'.

### Solution:
```java
class Solution {
    public boolean isPathCrossing(String path) {
        Set<String> s = new HashSet<>();
        s.add("0,0");
        int x = 0, y = 0;
        for(char c : path.toCharArray()){
            if(c == 'N') y++;
            else if(c == 'E') x++;
            else if(c == 'S') y--;
            else x--;
            String str = ""+x+","+y;
            if(s.contains(str)) return true;
            s.add(str);

        }
        return false;
    }
}
```
##### Faster using string Builder
```java
class Solution {
    public boolean isPathCrossing(String path) {
        Set<String> s = new HashSet<>();
        s.add("0,0");
        int x = 0, y = 0;
        StringBuilder sb = new StringBuilder();
        for(char c : path.toCharArray()){
            sb.setLength(0);
            if(c == 'N') y++;
            else if(c == 'E') x++;
            else if(c == 'S') y--;
            else x--;
            if(!s.add(sb.append(x).append(",").append(y).toString())) return true;

        }
        return false;
    }
}
```