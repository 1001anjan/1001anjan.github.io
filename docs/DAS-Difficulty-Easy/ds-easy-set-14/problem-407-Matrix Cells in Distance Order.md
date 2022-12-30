---
layout: default
title: Matrix Cells in Distance Order
parent: Easy Set 14
grand_parent: DSA Easy Difficulty
nav_order: 7
permalink: /problem-407-Matrix Cells in Distance Order/
---
# Matrix Cells in Distance Order
You are given four integers row, cols, rCenter, and cCenter. There is a rows x cols matrix and you are on the cell with the coordinates (rCenter, cCenter).

Return the coordinates of all cells in the matrix, sorted by their distance from (rCenter, cCenter) from the smallest distance to the largest distance. You may return the answer in any order that satisfies this condition.

The distance between two cells (r1, c1) and (r2, c2) is |r1 - r2| + |c1 - c2|.

##### Example 1:
```markdown
Input: rows = 1, cols = 2, rCenter = 0, cCenter = 0
Output: [[0,0],[0,1]]
Explanation: The distances from (0, 0) to other cells are: [0,1]
```
##### Example 2:
```markdown
Input: rows = 2, cols = 2, rCenter = 0, cCenter = 1
Output: [[0,1],[0,0],[1,1],[1,0]]
Explanation: The distances from (0, 1) to other cells are: [0,1,1,2]
The answer [[0,1],[1,1],[0,0],[1,0]] would also be accepted as correct.
```
##### Example 3:
```markdown
Input: rows = 2, cols = 3, rCenter = 1, cCenter = 2
Output: [[1,2],[0,2],[1,1],[0,1],[1,0],[0,0]]
Explanation: The distances from (1, 2) to other cells are: [0,1,1,2,2,3]
There are other answers that would also be accepted as correct, such as [[1,2],[1,1],[0,2],[1,0],[0,1],[0,0]].
```
##### Constraints:
* 1 <= rows, cols <= 100
* 0 <= rCenter < rows
* 0 <= cCenter < cols

### Solution:
Using Sorting: 
```java
class Solution {
    public int[][] allCellsDistOrder(int rows, int cols, int rCenter, int cCenter) {
        int[][] ans = new int[rows*cols][2];
        int k = 0;
        for(int i = 0; i < rows; i++){
            for(int j = 0; j < cols; j++){
               ans[k][0] = i;
                ans[k][1] = j;
                k++;
            }
        }
        
        // sort the array
        Arrays.sort(ans, (a,b) ->{
            int d1 = Math.abs(a[0] - rCenter) + Math.abs(a[1] - cCenter);
            int d2 = Math.abs(b[0] - rCenter) + Math.abs(b[1] - cCenter);
            return d1 - d2;
        });
        
        return ans;
    }
}
```
Using BFS but slow execution
```java
class Solution {
    public int[][] allCellsDistOrder(int rows, int cols, int rCenter, int cCenter) {
        int[][] ans = new int[rows*cols][2];
        Queue<int[]> queue = new LinkedList<>();
        boolean[][] visited = new boolean[rows][cols];
        queue.offer(new int[]{rCenter,cCenter});
        int k = 0;
        while(!queue.isEmpty()){
            int[] item = queue.poll();
            if(item[0] < 0 || item[0] >= rows || item[1] < 0 || item[1] >= cols) continue;
            if(visited[item[0]][item[1]]) continue;
            
            visited[item[0]][item[1]] = true;
            ans[k++] = item;
            
            queue.offer(new int[]{item[0], item[1] + 1});
            queue.offer(new int[]{item[0], item[1] - 1});
            queue.offer(new int[]{item[0] + 1, item[1]});
            queue.offer(new int[]{item[0] - 1, item[1]});
        }
        
        return ans;
    }
}
```