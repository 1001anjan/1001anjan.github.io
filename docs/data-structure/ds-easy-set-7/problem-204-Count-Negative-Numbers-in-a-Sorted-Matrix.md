---
layout: default
title: Count Negative Numbers in a Sorted Matrix
parent: Data Structure Easy Set 7
grand_parent: Data Structure
nav_order: 14
permalink: /problem-204-Count-Negative-Numbers-in-a-Sorted-Matrix/
---
# Count Negative Numbers in a Sorted Matrix
Given a m x n matrix grid which is sorted in non-increasing order both row-wise and column-wise, return the number of negative numbers in grid.

##### Example 1:
```markdown
Input: grid = [[4,3,2,-1],[3,2,1,-1],[1,1,-1,-2],[-1,-1,-2,-3]]
Output: 8
Explanation: There are 8 negatives number in the matrix.
```
##### Example 2:
```markdown
Input: grid = [[3,2],[1,0]]
Output: 0
```
##### Constraints:
* m == grid.length
* n == grid[i].length
* 1 <= m, n <= 100
* -100 <= grid[i][j] <= 100

Follow up: Could you find an O(n + m) solution?

### Solution: 
#### Time Complexity O(m*n)
```java
class Solution {
    public int countNegatives(int[][] grid) {
        int count = 0;
        for(int i = 0; i <grid.length; i++){
            for(int j = grid[i].length - 1; j>=0; j--){
                if(grid[i][j] < 0) count++;
                else break;
            }
        }
        return count;
    }
}
```
#### Time Complexity O(m*logN) but actually consumed more time than first approach
```java
class Solution {
    public int countNegatives(int[][] grid) {
        int count = 0;
        for(int i = 0; i <grid.length; i++){
            if(grid[i][grid[i].length - 1] < 0)
                count += grid[i].length - binarySearch(grid[i]);
            System.out.println(count);
        }
        return count;
    }
    
    public int binarySearch(int[] arr){
        int s = 0;
        int e = arr.length - 1;
        while(s <= e){
            int mid = (s+e)/2;
            if(mid == 0 && arr[mid] < 0) return mid;
            if(mid == arr.length - 1) return mid;
            if(mid == 0 && arr[mid] >= 0) s = mid + 1;
            
            else if(arr[mid - 1]>=0 && arr[mid] < 0) return mid;
            else if(arr[mid - 1] < 0) e = mid - 1;
            else
                s = mid + 1;
            
        }
        throw null;
    }
}
```
#### Time Complexity: O(m+n) and much faster
```java
class Solution {
    public int countNegatives(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int i = 0;
        int j = n-1;

        int count = 0; 
        while(i<=m-1 && j>=0)
        {
            if(grid[i][j] < 0)
            {
                count += m-i; 

                j--;
            }else{
                i++;
            }
        }
        return count;
    }
}
```

