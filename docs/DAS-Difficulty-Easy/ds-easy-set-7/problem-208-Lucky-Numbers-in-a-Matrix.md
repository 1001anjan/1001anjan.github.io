---
layout: default
title: Lucky Numbers in a Matrix
parent: Easy Set 7
grand_parent: DSA Easy
nav_order: 18
permalink: /problem-208-Lucky-Numbers-in-a-Matrix/
---
# Lucky Numbers in a Matrix

Given an m x n matrix of distinct numbers, return all lucky numbers in the matrix in any order.

A lucky number is an element of the matrix such that it is the minimum element in its row and maximum in its column.

##### Example 1:
```markdown
Input: matrix = [[3,7,8],[9,11,13],[15,16,17]]
Output: [15]
Explanation: 15 is the only lucky number since it is the minimum in its row and the maximum in its column.
```

##### Example 2:
```markdown
Input: matrix = [[1,10,4,2],[9,3,8,7],[15,16,17,12]]
Output: [12]
Explanation: 12 is the only lucky number since it is the minimum in its row and the maximum in its column.
```

##### Example 3:
```markdown
Input: matrix = [[7,8],[1,2]]
Output: [7]
Explanation: 7 is the only lucky number since it is the minimum in its row and the maximum in its column.
```
##### Constraints:
* m == mat.length
* n == mat[i].length
* 1 <= n, m <= 50
* 1 <= matrix[i][j] <= 105.
* All elements in the matrix are distinct.

### Solution:
```java
class Solution {
    public List<Integer> luckyNumbers (int[][] matrix) {
        List<Integer> ans = new ArrayList<>();
        for(int i = 0; i < matrix.length; i++){
            // find min value
            int min = matrix[i][0];
            int index = 0;
            for(int j = 1; j < matrix[i].length; j++){
                if(min > matrix[i][j]){
                    min = matrix[i][j];
                    index = j;
                }
            }
            // check if (min) is the  max value
            boolean f = true;
            for(int j = 0; j < matrix.length; j++){
                if(min < matrix[j][index]){
                    f = false;
                    break;
                }
            }
            // add element to the list
            if(f) ans.add(min);
        }
        
        return ans;
    }
}
```