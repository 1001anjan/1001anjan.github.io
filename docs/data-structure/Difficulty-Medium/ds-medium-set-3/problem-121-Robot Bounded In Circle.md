---
layout: default
title: Robot Bounded In Circle
parent: Data Structure Medium Set 3
grand_parent: Data Structure
nav_order: 21
permalink: /problem-121-Robot Bounded In Circle/
---
# Robot Bounded In Circle
On an infinite plane, a robot initially stands at (0, 0) and faces north. Note that:

* The north direction is the positive direction of the y-axis.
* The south direction is the negative direction of the y-axis.
* The east direction is the positive direction of the x-axis.
* The west direction is the negative direction of the x-axis.
* The robot can receive one of three instructions:

* "G": go straight 1 unit.
* "L": turn 90 degrees to the left (i.e., anti-clockwise direction).
* "R": turn 90 degrees to the right (i.e., clockwise direction).
* The robot performs the instructions given in order, and repeats them forever.

Return true if and only if there exists a circle in the plane such that the robot never leaves the circle.

##### Example 1:
```markdown
Input: instructions = "GGLLGG"
Output: true
Explanation: The robot is initially at (0, 0) facing the north direction.
"G": move one step. Position: (0, 1). Direction: North.
"G": move one step. Position: (0, 2). Direction: North.
"L": turn 90 degrees anti-clockwise. Position: (0, 2). Direction: West.
"L": turn 90 degrees anti-clockwise. Position: (0, 2). Direction: South.
"G": move one step. Position: (0, 1). Direction: South.
"G": move one step. Position: (0, 0). Direction: South.
Repeating the instructions, the robot goes into the cycle: (0, 0) --> (0, 1) --> (0, 2) --> (0, 1) --> (0, 0).
Based on that, we return true.
```
##### Example 2:
```markdown
Input: instructions = "GG"
Output: false
Explanation: The robot is initially at (0, 0) facing the north direction.
"G": move one step. Position: (0, 1). Direction: North.
"G": move one step. Position: (0, 2). Direction: North.
Repeating the instructions, keeps advancing in the north direction and does not go into cycles.
Based on that, we return false.
```
##### Example 3:
```markdown
Input: instructions = "GL"
Output: true
Explanation: The robot is initially at (0, 0) facing the north direction.
"G": move one step. Position: (0, 1). Direction: North.
"L": turn 90 degrees anti-clockwise. Position: (0, 1). Direction: West.
"G": move one step. Position: (-1, 1). Direction: West.
"L": turn 90 degrees anti-clockwise. Position: (-1, 1). Direction: South.
"G": move one step. Position: (-1, 0). Direction: South.
"L": turn 90 degrees anti-clockwise. Position: (-1, 0). Direction: East.
"G": move one step. Position: (0, 0). Direction: East.
"L": turn 90 degrees anti-clockwise. Position: (0, 0). Direction: North.
Repeating the instructions, the robot goes into the cycle: (0, 0) --> (0, 1) --> (-1, 1) --> (-1, 0) --> (0, 0).
Based on that, we return true.
```
##### Constraints:
* 1 <= instructions.length <= 100
* instructions[i] is 'G', 'L' or, 'R'.

### Solution:
```java
class Solution {
    public boolean isRobotBounded(String instructions) {
        int[] pos = new int[]{0,0};
        char curr = 'N';
        for(char ch : instructions.toCharArray()){
            switch(ch){
                case 'G' : move(pos, curr); break;
                case 'R' :
                case 'L' : curr = changeDirection(curr, ch); break;
            }
        }
        if(pos[0] == 0 && pos[1] == 0) return true;
        if(curr == 'N' && !(pos[0] == 0 && pos[1] == 0)) return false;
        return true;

    }

    public void move(int[] pos, char dir){
        switch(dir){
            case 'N' : pos[1]++; break;
            case 'S' : pos[1]--; break;
            case 'E' : pos[0]++; break;
            case 'W' : pos[0]--; break;
        }
    }

    public char changeDirection(char curr, char ins){

        switch(curr){
            case 'N' : return ins == 'L'? 'W' : 'E';
            case 'S' : return ins == 'L'? 'E' : 'W';
            case 'E' : return ins == 'L'? 'N' : 'S';
            case 'W' : return ins == 'L'? 'S' : 'N';
        }
        throw null;
    }
}
```
```markdown
Let chopper help explain.

Starting at the origin and face north (0,1),
after one sequence of instructions,

if chopper return to the origin, he is obvious in an circle.
if chopper finishes with face not towards north,
it will get back to the initial status in another one or three sequences.
Explanation
(x,y) is the location of chopper.
d[i] is the direction he is facing.
i = (i + 1) % 4 will turn right
i = (i + 3) % 4 will turn left
Check the final status after instructions.
```

##### Complexity
Time O(N)
Space O(1)

```java
class Solution {
    public boolean isRobotBounded(String ins) {
        int x = 0, y = 0, i = 0, d[][] = {
                {0, 1}, {1, 0}, {0, -1}, {-1, 0}
        };
        for (int j = 0; j < ins.length(); ++j)
            if (ins.charAt(j) == 'R')
                i = (i + 1) % 4;
            else if (ins.charAt(j) == 'L')
                i = (i + 3) % 4;
            else {
                x += d[i][0];
                y += d[i][1];
            }
        return x == 0 && y == 0 || i > 0;
    }
}
```