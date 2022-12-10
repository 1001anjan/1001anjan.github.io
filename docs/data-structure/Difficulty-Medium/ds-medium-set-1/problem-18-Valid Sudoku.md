---
layout: default
title: Valid Sudoku
parent: Data Structure Medium Set 1
grand_parent: Data Structure
nav_order: 18
permalink: /problem-18-Valid Sudoku/
---
# Valid Sudoku
Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

Each row must contain the digits 1-9 without repetition.
Each column must contain the digits 1-9 without repetition.
Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.
Note:

* A Sudoku board (partially filled) could be valid but is not necessarily solvable.
* Only the filled cells need to be validated according to the mentioned rules.

![](../../assets/images/ds/Sudoku-by-L2G-20050714.svg.png)

##### Example 1:
```markdown
Input: board =
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```
##### Example 2:
```markdown
Input: board =
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```
##### Constraints:
* board.length == 9
* board[i].length == 9
* board[i][j] is a digit 1-9 or '.'.

### Solution:
```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        Set<Character> row = new HashSet<>();
        Set<Character> col = new HashSet<>();
        Set<Character> cube = new HashSet<>();
        for(int i = 0; i < 9; i++){
            row.clear();
            col.clear();
            cube.clear();
            for(int j = 0; j < 9; j++){
                if(board[i][j] != '.' && !row.add(board[i][j])) return false;
                if(board[j][i] != '.' && !col.add(board[j][i])) return false;

                int ci = 3*(i/3) + (j/3);
                int cj = 3*(i%3) + (j%3);
                if(board[ci][cj] != '.' && !cube.add(board[ci][cj])) return false;
            }
        }

        return true;
    }
}
```
