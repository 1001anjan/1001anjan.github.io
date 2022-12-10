---
layout: default
title: Combinations
parent: Data Structure Medium Set 1
grand_parent: Data Structure
nav_order: 42
permalink: /problem-42-Combinations/
---
# Combinations
Given two integers n and k, return all possible combinations of k numbers chosen from the range [1, n].

You may return the answer in any order.

##### Example 1:
```markdown
Input: n = 4, k = 2
Output: [[1,2],[1,3],[1,4],[2,3],[2,4],[3,4]]
Explanation: There are 4 choose 2 = 6 total combinations.
Note that combinations are unordered, i.e., [1,2] and [2,1] are considered to be the same combination.
```
##### Example 2:
```markdown
Input: n = 1, k = 1
Output: [[1]]
Explanation: There is 1 choose 1 = 1 total combination.
```
##### Constraints:
* 1 <= n <= 20
* 1 <= k <= n

### Solution:
```java
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> ans = new ArrayList<>();
        process(1, n, k, ans, new ArrayList<>());
        return ans;
    }

    public void process(int start, int n, int k, List<List<Integer>> ans, List<Integer> list){
        if(list.size() > k) return;
        if(list.size() == k){
            ans.add(new ArrayList<>(list));
            return;
        }
        for(int i = start; i <= n; i++){
            list.add(i);
            process(i + 1, n, k, ans, list);
            list.remove(list.size() - 1);
        }
    }
}
```