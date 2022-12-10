---
layout: default
title: Cousins in Binary Tree
parent: Data Structure Easy Set 5
grand_parent: Data Structure
nav_order: 29
permalink: /problem-159-Cousins-in-Binary-Tree/
---
# Find the Town Judge
In a town, there are n people labeled from 1 to n. There is a rumor that one of these people is secretly the town judge.

If the town judge exists, then:

* The town judge trusts nobody.
* Everybody (except for the town judge) trusts the town judge.
* There is exactly one person that satisfies properties 1 and 2.

You are given an array trust where trust[i] = [ai, bi] representing that the person labeled ai trusts the person labeled bi.

Return the label of the town judge if the town judge exists and can be identified, or return -1 otherwise.

##### Example 1:
```markdown
Input: n = 2, trust = [[1,2]]
Output: 2
```
##### Example 2:
```markdown
Input: n = 3, trust = [[1,3],[2,3]]
Output: 3
```
##### Example 3:
```markdown
Input: n = 3, trust = [[1,3],[2,3],[3,1]]
Output: -1
```
##### Constraints:
* 1 <= n <= 1000
* 0 <= trust.length <= 104
* trust[i].length == 2
* All the pairs of trust are unique.
* ai != bi
* 1 <= ai, bi <= n

### Solution:
```java
class Solution {
    public int findJudge(int n, int[][] trust) {
        boolean[] s = new boolean[n];
        int[] c = new int[n];
        for(int i=0; i<trust.length; i++){
            s[trust[i][0]-1] = true;
            c[trust[i][1]-1]++;
        }
        for(int i=0; i<n; i++)
            if(!s[i] && c[i] == n-1) return i+1;
        return -1;
    }
}
```