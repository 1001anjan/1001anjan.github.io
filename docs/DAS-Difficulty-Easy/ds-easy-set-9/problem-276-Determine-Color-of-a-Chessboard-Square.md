---
layout: default
title: Determine Color of a Chessboard Square
parent: Easy Set 9
grand_parent: DSA Easy Difficulty
nav_order: 26
permalink: /problem-276-Determine-Color-of-a-Chessboard-Square/
---
# Determine Color of a Chessboard Square
You are given coordinates, a string that represents the coordinates of a square of the chessboard. Below is a chessboard for your reference.

Return true if the square is white, and false if the square is black.

The coordinate will always represent a valid chessboard square. The coordinate will always have the letter first, and the number second.

![](../../assets/images/ds/screenshot-2021-02-20-at-22159-pm.png)

##### Example 1:
```markdown
Input: coordinates = "a1"
Output: false
Explanation: From the chessboard above, the square with coordinates "a1" is black, so return false.
```
##### Example 2:
```markdown
Input: coordinates = "h3"
Output: true
Explanation: From the chessboard above, the square with coordinates "h3" is white, so return true.
```
##### Example 3:
```markdown
Input: coordinates = "c7"
Output: false
```
##### Constraints:
* coordinates.length == 2
* 'a' <= coordinates[0] <= 'h'
* '1' <= coordinates[1] <= '8'

### Solution:
```java
class Solution {
    public boolean squareIsWhite(String coordinates) {
        return (getRefvalue(coordinates.charAt(0)) ^ ((coordinates.charAt(1) - '0')%2)) == 1;
    }
    
    public int getRefvalue(char c){
        switch(c){
            case 'a','c','e','g': return 1;
            default: return 0;
        }
    }
}
```
###### Another way
```java
class Solution {
    public boolean squareIsWhite(String coordinates) {
        int coord = coordinates.charAt(0) - 97 + coordinates.charAt(1) - 48;
        return coord % 2 == 0 ? true : false;
    }
}
```