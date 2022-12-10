---
layout: default
title: Pascal's Triangle
parent: Data Structure Easy Set 13
grand_parent: Data Structure
nav_order: 4
permalink: /problem-374-Pascal's Triangle/
---
# Pascal's Triangle
Given an integer numRows, return the first numRows of Pascal's triangle.

In Pascal's triangle, each number is the sum of the two numbers directly above it as shown:
![](../../assets/images/ds/PascalTriangleAnimated22.gif)
##### Example 1:
```markdown
Input: numRows = 5
Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
```
##### Example 2:
```markdown
Input: numRows = 1
Output: [[1]]
```
##### Constraints:
* 1 <= numRows <= 30

### Solution:
```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> ans = new ArrayList<>();
        List<Integer> prev = null, curr = null;
        for(int i = 0; i < numRows; i++){
            curr = new ArrayList<>();
            for(int j = 0; j <= i; j++){
                if(j == 0 || j == i){
                    curr.add(1);
                }else{
                    curr.add(prev.get(j - 1) + prev.get(j));
                }
            }
            prev = curr;
            ans.add(curr);
        }
        return ans;
    }
}
```