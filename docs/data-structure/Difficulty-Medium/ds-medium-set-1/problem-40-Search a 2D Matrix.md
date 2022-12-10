---
layout: default
title: Search a 2D Matrix
parent: Data Structure Medium Set 1
grand_parent: Data Structure
nav_order: 40
permalink: /problem-40-Search a 2D Matrix/
---
# Search a 2D Matrix
Write an efficient algorithm that searches for a value target in an m x n integer matrix matrix. This matrix has the following properties:

* Integers in each row are sorted from left to right.
* The first integer of each row is greater than the last integer of the previous row.

##### Example 1:
![](../../assets/images/ds/mat999.jpeg)
```markdown
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```
##### Example 2:
![](../../assets/images/ds/mat999.jpeg)
```markdown
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false
```
##### Constraints:
* m == matrix.length
* n == matrix[i].length
* 1 <= m, n <= 100
* -10^4 <= matrix[i][j], target <= 10^4

### Solution:
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int n = matrix[0].length - 1;

        for(int[] arr : matrix){
            if(arr[0] == target || target == arr[n]) return true;
            if(arr[0] < target && target < arr[n]) return binarySearch(arr, 0, n, target);
        }

        return false;
    }

    public boolean binarySearch(int[] arr, int l, int u, int target){
        if(l > u) return false;
        int m = (l + u)/2;
        if(arr[m] == target) return true;
        if(arr[m] > target) return binarySearch(arr, l, m - 1, target); 
        else return binarySearch(arr, m + 1, u, target);
    }
}
```

