---
layout: default
title: Number of Equivalent Domino Pairs
parent: Easy Set 6
grand_parent: DSA Easy
nav_order: 17
permalink: /problem-177-Number-of-Equivalent-Domino-Pairs/
---
# Number of Equivalent Domino Pairs

Given a list of dominoes, dominoes[i] = [a, b] is equivalent to dominoes[j] = [c, d] if and only if either (a == c and b == d), or (a == d and b == c) - that is, one domino can be rotated to be equal to another domino.

Return the number of pairs (i, j) for which 0 <= i < j < dominoes.length, and dominoes[i] is equivalent to dominoes[j].

##### Example 1:
```markdown
Input: dominoes = [[1,2],[2,1],[3,4],[5,6]]
Output: 1
```
##### Example 2:
```markdown
Input: dominoes = [[1,2],[1,2],[1,1],[1,2],[2,2]]
Output: 3
```
##### Constraints:
* 1 <= dominoes.length <= 4 * 104
* dominoes[i].length == 2
* 1 <= dominoes[i][j] <= 9

### Solution:
```java
class Solution {
    public int numEquivDominoPairs(int[][] dominoes) {
        int count = 0;
        Map<Integer, Integer> m = new HashMap<>();

        for(int i = 0; i < dominoes.length ; i++){
            int max = Math.max(dominoes[i][0],dominoes[i][1]);
            int min = Math.min(dominoes[i][0],dominoes[i][1]);
            int key = max*10 + min;
            count += m.getOrDefault(key,0);
            m.put(key, m.getOrDefault(key,0)+1);
        }

        return count;
    }
}
```
