---
layout: default
title: Surrounded Regions
parent: Medium Set 4
grand_parent: DSA Medium Difficulty
nav_order: 11
permalink: /problem-161-Surrounded Regions/
---
# Surrounded Regions
Given an m x n matrix board containing 'X' and 'O', capture all regions that are 4-directionally surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

##### Example 1:
![](../../assets/images/ds/xogrid22.jpeg)
```markdown
Input: board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
Output: [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
Explanation: Notice that an 'O' should not be flipped if:
- It is on the border, or
- It is adjacent to an 'O' that should not be flipped.
  The bottom 'O' is on the border, so it is not flipped.
  The other three 'O' form a surrounded region, so they are flipped.
```
##### Example 2:
```markdown
Input: board = [["X"]]
Output: [["X"]]
```
##### Constraints:
* m == board.length
* n == board[i].length
* 1 <= m, n <= 200
* board[i][j] is 'X' or 'O'.

### Solution:
##### Time Complexity: O(n^3)
```java
class Solution {
    boolean ss;
    public void solve(char[][] board) {
        List<int[]> list = new ArrayList<>();
        Set<String> visited = new HashSet<>();

        for(int i = 1; i < board.length - 1; i++){
            for(int j = 1; j < board[0].length - 1; j++){
                if(board[i][j] == 'O'){
                    ss = true;
                    process(board, i, j, list, visited);
                    if(ss) for(int[] arr : list) board[arr[0]][arr[1]] = 'X';
                }
                list.clear();
                visited.clear();
            }
        }
    }

    public void process(char[][] board, int i , int j, List<int[]> list, Set<String> visited){
        if(i < 0 || i > board.length || j < 0 || j > board[0].length){
            ss =  ss && false;
            return;
        }
        if(i == 0 && board[i][j] == 'O') {
            ss =  ss && false;
            return;
        }
        if(j == 0 && board[i][j] == 'O') {
            ss =  ss && false;
            return;
        }
        if(i == board.length - 1 && board[i][j] == 'O') {
            ss =  ss && false;
            return;
        }
        
        if(j == board[0].length - 1 && board[i][j] == 'O') {
            ss =  ss && false;
            return;
        }
        
        visited.add(i+"-"+j);
        list.add(new int[]{i, j});

        if(i - 1 >= 0 && board[i - 1][j] == 'O' && !visited.contains((i - 1)+"-"+j)) 
            process(board, i - 1, j, list, visited);

        if(j - 1 >= 0 && board[i][j - 1] == 'O' && !visited.contains(i+"-"+(j - 1))) 
            process(board, i, j - 1, list, visited);
        
        if(i + 1 < board.length && board[i + 1][j] == 'O' && !visited.contains((i + 1)+"-"+j)) 
            process(board, i + 1, j, list, visited);

        if(j + 1 < board[0].length && board[i][j + 1] == 'O' && !visited.contains(i+"-"+(j + 1))){
            process(board, i, j + 1, list, visited);

        } 
         ss =  ss && true;  
    }
}
```
##### Improvement: O(n^2)
Basically, all the boundary 'O's need not to be changed.
Use DFS to visit the boundary 'O', turn it into 'V' and explore the node.
In this way, we change the remaining 'O's to 'X's.
Convert the 'V's to 'O's.
```java
class Solution {
    public void solve(char[][] board) {
        int rows = board.length;
        int cols = board[0].length;
        for(int i = 0; i < rows; i++){
            for(int j = 0; j < cols; j++){
                if(i * j == 0 || i == rows-1 || j == cols-1){ 
            //We check for Boundary 'O's and turn them into 'V'.
            //These are valid 'O's and need not to be changed to 'X's.
                    if(board[i][j] == 'O'){
                        dfs(board, i, j);
                    }
                }
            }
        }
//Iterate over the whole grid, change remaining 'O's to 'X's.
//Change 'V's to 'O's
        for(int i = 0; i < rows; i++){
            for(int j = 0; j < cols; j++){
                if(board[i][j] == 'O'){
                    board[i][j] = 'X';
                }
                else if(board[i][j] == 'V'){
                    board[i][j] = 'O';
                }
            }
        }
    }

//Main DFS Function to convert all the boundary 'O's to 'V's

    private void dfs(char[][] board, int i, int j){
        if(i < 0 || j < 0 || i >= board.length || j >= board[0].length || board[i][j] != 'O'){
            return;
        }
        board[i][j] = 'V';
        dfs(board, i + 1, j);
        dfs(board, i - 1, j);
        dfs(board, i, j + 1);
        dfs(board, i, j - 1);
    }

}
```