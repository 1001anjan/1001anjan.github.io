---
layout: default
title: Triangle
parent: Data Structure Medium Set 2
grand_parent: Data Structure
nav_order: 32
permalink: /problem-82-Triangle/
---
# Triangle
Given a triangle array, return the minimum path sum from top to bottom.

For each step, you may move to an adjacent number of the row below. More formally, if you are on index i on the current row, you may move to either index i or index i + 1 on the next row.

##### Example 1:
```markdown
Input: triangle = [[2],[3,4],[6,5,7],[4,1,8,3]]
Output: 11
Explanation: The triangle looks like:
2
3 4
6 5 7
4 1 8 3
The minimum path sum from top to bottom is 2 + 3 + 5 + 1 = 11 (underlined above).
```
##### Example 2:
```markdown
Input: triangle = [[-10]]
Output: -10
```
##### Constraints:
* 1 <= triangle.length <= 200
* triangle[0].length == 1
* triangle[i].length == triangle[i - 1].length + 1
* -10^4 <= triangle[i][j] <= 10^4

##### Follow up: Could you do this using only O(n) extra space, where n is the total number of rows in the triangle?

### Solution: 

###### Time Limit Exceeded
```java
class Solution {
    int min = Integer.MAX_VALUE;
    public int minimumTotal(List<List<Integer>> triangle) {
        processTriangle(triangle, 0, 0, 0);
        return min;
    }

    public void processTriangle(List<List<Integer>> triangle, int pos, int sum, int level){
        if(level > triangle.size()) return;
        if(level == triangle.size()){
            if(sum < min) min = sum;
            return;
        }
        List<Integer> l = triangle.get(level);
        if(pos < l.size()){
            processTriangle(triangle, pos, sum + l.get(pos), level + 1);
        }
        if(pos + 1 < l.size()){
            processTriangle(triangle, pos + 1, sum + l.get(pos + 1), level + 1);
        }
    }
}
```

##### Dynamic programming:
```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int m = triangle.size();

        // buttom row
        List<Integer> list = triangle.get(m - 1);
        int n = list.size();
        int[] dp = new int[n];

        // initializing buttom row 
        for(int i = 0; i < n ; i++) dp[i] = list.get(i);

        // processing dp
        for(int i = m - 2; i >= 0; i--){
            list = triangle.get(i);
            for(int j = 0; j <= i; j++){
                int v = list.get(j);
                dp[j] = Math.min(v + dp[j], v + dp[j + 1]);
            }
        }

        return dp[0];
    }

}
```