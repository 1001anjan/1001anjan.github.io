---
layout: default
title: Word Search
parent: Data Structure Medium Set 1
grand_parent: Data Structure
nav_order: 44
permalink: /problem-44-Word Search/
---
# Word Search
Given an m x n grid of characters board and a string word, return true if word exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

##### Example 1:
![](../../assets/images/ds/word2.jpeg)

```markdown
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```
##### Example 2:
![](../../assets/images/ds/word-1.jpeg![img.png](img.png))

```markdown
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
Output: true
```
##### Example 3:
![](../../assets/images/ds/word3.jpeg)

```markdown
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
Output: false
```
##### Constraints:
* m == board.length
* n = board[i].length
* 1 <= m, n <= 6
* 1 <= word.length <= 15
* board and word consists of only lowercase and uppercase English letters.


Follow up: Could you use search pruning to make your solution faster with a larger board?

### Solution:
```java
class Solution {
    public boolean exist(char[][] board, String word) {
        boolean[][] visited = new boolean[board.length][board[0].length];
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[0].length; j++){
                if(search(board, i, j, 0, word.toCharArray(), visited)) return true;
            }
        }
        return false;
    }

    public boolean search(char[][] board, int i, int j, int index, char[] word, boolean[][] visited){
        if(index >= word.length) return true;
        if(board[i][j] != word[index]) return false;
        if(board[i][j] == word[index] && index == word.length - 1) return true;
        if(i < 0 || j < 0 || i >= board.length || j >= board[0].length) return false;
        visited[i][j] = true;
        boolean status1, status2, status3, status4;
        status1 = status2 = status3 = status4 = false;
        if(i > 0 && !visited[i - 1][j]){
            status1 = search(board, i - 1, j, index + 1, word, visited);
            visited[i - 1][j] = false;
        }
        if(j > 0 && !visited[i][j - 1]){
            status2 = search(board, i, j - 1, index + 1, word, visited);
            visited[i][j - 1] = false;
        }
        if(i + 1 < board.length && !visited[i + 1][j]){
            status3 = search(board, i + 1, j, index + 1, word, visited);
            visited[i + 1][j] = false;
        }
        if(j + 1< board[0].length && !visited[i][j + 1]){
            status4 = search(board, i, j + 1, index + 1, word, visited);
            visited[i][j + 1] = false;
        }
        visited[i][j] = false;
        return status1 | status2 | status3 | status4;
    }
}
```