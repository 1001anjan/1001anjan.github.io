---
layout: default
title: Pascal's Triangle
parent: Easy Set 13
grand_parent: DSA Easy
nav_order: 5
permalink: /problem-375-Pascal's Triangle II/
---
# Pascal's Triangle II
Given an integer rowIndex, return the rowIndexth (0-indexed) row of the Pascal's triangle.

In Pascal's triangle, each number is the sum of the two numbers directly above it as shown:
![](../../assets/images/ds/PascalTriangleAnimated22.gif)
##### Example 1:
```markdown
Input: rowIndex = 3
Output: [1,3,3,1]
```
##### Example 2:
```markdown
Input: rowIndex = 0
Output: [1]
```
##### Example 3:
```markdown
Input: rowIndex = 1
Output: [1,1]
```
##### Constraints:
* 0 <= rowIndex <= 33

### Solution:
```java
class Solution {
    
    //  Time Complexity = O(N*N) (approximation)
    //  Space Complexity = O(N)
    
    public List<Integer> getRow(int rowIndex) {
        List<Integer> result = new ArrayList<Integer>();
        
        for (int row = 0; row <= rowIndex; row++) {
            result.add(0, 1);
            for (int i = 1; i < row; i++)
                result.set(i, result.get(i) + result.get(i + 1));
        }
        return result;
    }
}
```