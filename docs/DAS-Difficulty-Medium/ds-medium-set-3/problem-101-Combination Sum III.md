---
layout: default
title: Combination Sum III
parent: Medium Set 2
grand_parent: DSA Medium
nav_order: 1
permalink: /problem-101-Combination Sum III/
---
# Combination Sum III
Find all valid combinations of k numbers that sum up to n such that the following conditions are true:

* Only numbers 1 through 9 are used.
* Each number is used at most once.
Return a list of all possible valid combinations. The list must not contain the same combination twice, and the combinations may be returned in any order.

##### Example 1:
```markdown
Input: k = 3, n = 7
Output: [[1,2,4]]
Explanation:
1 + 2 + 4 = 7
There are no other valid combinations.
```
##### Example 2:
```markdown
Input: k = 3, n = 9
Output: [[1,2,6],[1,3,5],[2,3,4]]
Explanation:
1 + 2 + 6 = 9
1 + 3 + 5 = 9
2 + 3 + 4 = 9
There are no other valid combinations.
```
##### Example 3:
```markdown
Input: k = 4, n = 1
Output: []
Explanation: There are no valid combinations.
Using 4 different numbers in the range [1,9], the smallest sum we can get is 1+2+3+4 = 10 and since 10 > 1, there are no valid combination.
```
##### Constraints:
* 2 <= k <= 9
* 1 <= n <= 60

### Solution:
```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> ans = new ArrayList<>();
        proceesCombinationSum3(1, k, n, ans, new ArrayList<>());
        return ans;
    }

    private void proceesCombinationSum3(int start, int k, int target, List<List<Integer>> ans, List<Integer> list){
        if(list.size() > k || target < 0) return;
        if(list.size() == k && target == 0){
            ans.add(new ArrayList<>(list));
        }
        for(int i = start; i < 10; i++){
           list.add(i);
            proceesCombinationSum3(i + 1, k, target - i, ans, list);
            list.remove(list.size() - 1);
        } 
    }
}
```