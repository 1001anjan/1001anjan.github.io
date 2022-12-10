---
layout: default
title: Find Winner on a Tic Tac Toe Game
parent: Data Structure Easy Set 14
grand_parent: Data Structure
nav_order: 16
permalink: /problem-416-Find Winner on a Tic Tac Toe Game/
---
# Find Winner on a Tic Tac Toe Game
Tic-tac-toe is played by two players A and B on a 3 x 3 grid. The rules of Tic-Tac-Toe are:

* Players take turns placing characters into empty squares ' '.
* The first player A always places 'X' characters, while the second player B always places 'O' characters.
* 'X' and 'O' characters are always placed into empty squares, never on filled ones.
* The game ends when there are three of the same (non-empty) character filling any row, column, or diagonal.
* The game also ends if all squares are non-empty.
* No more moves can be played if the game is over.
Given a 2D integer array moves where moves[i] = [rowi, coli] indicates that the ith move will be played on grid[rowi][coli]. return the winner of the game if it exists (A or B). In case the game ends in a draw return "Draw". If there are still movements to play return "Pending".

You can assume that moves is valid (i.e., it follows the rules of Tic-Tac-Toe), the grid is initially empty, and A will play first.

##### Example 1:
![](../../assets/images/ds/xo1-grid.jpeg)
```markdown
Input: moves = [[0,0],[2,0],[1,1],[2,1],[2,2]]
Output: "A"
Explanation: A wins, they always play first.
```
##### Example 2:
![](../../assets/images/ds/xo2-grid.jpeg![img.png](img.png))
```markdown
Input: moves = [[0,0],[1,1],[0,1],[0,2],[1,0],[2,0]]
Output: "B"
Explanation: B wins.
```
##### Example 3:
![](../../assets/images/ds/xo3-grid.jpeg)
```markdown
Input: moves = [[0,0],[1,1],[2,0],[1,0],[1,2],[2,1],[0,1],[0,2],[2,2]]
Output: "Draw"
Explanation: The game ends in a draw since there are no moves to make.
```
##### Constraints:
* 1 <= moves.length <= 9
* moves[i].length == 2
* 0 <= rowi, coli <= 2
* There are no repeated elements on moves.
* moves follow the rules of tic tac toe.

### Solution:
There are 8 ways to win for each player:

* 3 columns
* 3 rows
* 2 diagonals
Players make moves one by one so all odd moves are for player A, even for B.
Now we just need to track if we reach 3 in any line for any of the players.
One array keeps all ways to win for each player:

* 0,1,2 - for rows
* 3,4,5 - for cols
* 6 - for diagonal top left - bottom right
* 7 - for diagonal top right - bottom left

```java
class Solution {
    public String tictactoe(int[][] moves) {
        int a[] = new int[8];
        int b[] = new int[8];
        
        boolean t = true;
        for(int m[] : moves){
            int p[] = t ? a : b;
            t = t ? false : true;
            p[m[0]]++;
            p[m[1] + 3]++;
            if(m[0] == m[1]) p[6]++;
            if(m[0] == 2 - m[1]) p[7]++;
        }
        
        for(int i = 0; i < 8 ; i++){
            if(a[i] == 3) return "A";
            if(b[i] == 3) return "B";
        }
        return moves.length == 9 ? "Draw" : "Pending";
    }
}
```

