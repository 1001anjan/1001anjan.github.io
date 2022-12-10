---
layout: default
title: Count Largest Group
parent: Data Structure Easy Set 14
grand_parent: Data Structure
nav_order: 18
permalink: /problem-418-Count Largest Group/
---
# Count Largest Group
You are given an integer n.

Each number from 1 to n is grouped according to the sum of its digits.

Return the number of groups that have the largest size.

##### Example 1:
```markdown
Input: n = 13
Output: 4
Explanation: There are 9 groups in total, they are grouped according sum of its digits of numbers from 1 to 13:
[1,10], [2,11], [3,12], [4,13], [5], [6], [7], [8], [9].
There are 4 groups with largest size.
```
##### Example 2:
```markdown
Input: n = 2
Output: 2
Explanation: There are 2 groups [1], [2] of size 1.
```
##### Constraints:
* 1 <= n <= 10^4

### Solution:
```java
class Solution {
    public int countLargestGroup(int n) {
        int count = 0;
        int[] dp = new int[n + 1];
        Map<Integer,Integer> map = new HashMap<>();
        
        for(int i = 1; i <= n; i++){
            dp[i] = i % 10 + dp[i/10];
            map.put(dp[i], map.getOrDefault(dp[i],0) + 1);
        }
        
        int max = 0;
        for(int key : map.keySet()){
            if(map.get(key) > max){
                count = 1;
                max = map.get(key);
            }else if(map.get(key) == max) count++;
        }
        
        return count;
    }
}
```