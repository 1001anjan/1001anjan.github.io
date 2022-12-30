---
layout: default
title: Perfect Squares
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 16
permalink: /problem-116-Perfect Squares/
---
# Perfect Squares
Given an integer n, return the least number of perfect square numbers that sum to n.

A perfect square is an integer that is the square of an integer; in other words, it is the product of some integer with itself. For example, 1, 4, 9, and 16 are perfect squares while 3 and 11 are not.

##### Example 1:
```markdown
Input: n = 12
Output: 3
Explanation: 12 = 4 + 4 + 4.
```
##### Example 2:
```markdown
Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.
```
##### Constraints:
* 1 <= n <= 10^4

### Solution: 
##### Time Limit Exceeded

```java
class Solution {
    public int numSquares(int n) {
        Queue<Integer> q = new LinkedList<>();
        int level = 0;
        q.offer(0);

        while(!q.isEmpty()){
            int size = q.size();
            Queue<Integer> q1 = new LinkedList<>();
            while(size -- > 0){
                int x = q.poll();
                for(int i = 1; i <= n; i++){
                    int v = x + i *i;
                    if(v == n) return level + 1;
                    if(v < n ) q1.offer(v);
                    else break;
                }
            }
            q = q1;
            level ++;
        }
        return level;
    }
}
```
```java
class Solution {
    public int numSquares(int n) {
        int max=(int)Math.sqrt(n);
        int res=Integer.MAX_VALUE;
        return dfs(n,res,max,0);
    }
    private int dfs(int target,int res,int num,int count){
        if(target==0){
            res=Math.min(res,count);
            return res;
        }
        
        for(int i=num;i>0;i--){
            int square=(int)Math.pow(i,2);
            if(square>target) continue;
            if(count+1<res) res=dfs(target-square,res,i,count+1);
        }
        return res;
    }
}
```