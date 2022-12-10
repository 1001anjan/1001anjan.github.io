---
layout: default
title: Last Stone Weight
parent: Data Structure Easy Set 6
grand_parent: Data Structure
nav_order: 8
permalink: /problem-168-Last-Stone-Weight/
---
# Last Stone Weight

You are given an array of integers stones where stones[i] is the weight of the ith stone.

We are playing a game with the stones. On each turn, we choose the heaviest two stones and smash them together. Suppose the heaviest two stones have weights x and y with x <= y. The result of this smash is:

* If x == y, both stones are destroyed, and
* If x != y, the stone of weight x is destroyed, and the stone of weight y has new weight y - x.
At the end of the game, there is at most one stone left.

Return the weight of the last remaining stone. If there are no stones left, return 0.

##### Example 1:
```markdown
Input: stones = [2,7,4,1,8,1]
Output: 1
Explanation:
We combine 7 and 8 to get 1 so the array converts to [2,4,1,1,1] then,
we combine 2 and 4 to get 2 so the array converts to [2,1,1,1] then,
we combine 2 and 1 to get 1 so the array converts to [1,1,1] then,
we combine 1 and 1 to get 0 so the array converts to [1] then that's the value of the last stone.
```
##### Example 2:
```markdown
Input: stones = [1]
Output: 1
```
##### Constraints:
* 1 <= stones.length <= 30
* 1 <= stones[i] <= 1000

### Solution:
```java
class Solution {
    public int lastStoneWeight(int[] stones) {
        Queue<Integer> q = new PriorityQueue<Integer>(Collections.reverseOrder());
        for(int n : stones) q.add(n);
        
        while(q.size() > 1){
            int x = q.poll();
            int y = q.poll();
            if(x != y) q.add(Math.abs(x - y));
        }
        
        if(q.size() == 0) return 0;
        return q.poll();
    }
}
```