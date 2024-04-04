---
layout: default
title: Lexicographical Numbers
parent: Medium Set 3
grand_parent: DSA Medium
nav_order: 46
permalink: /problem-146-Lexicographical Numbers/
---
# Lexicographical Numbers
Given an integer n, return all the numbers in the range [1, n] sorted in lexicographical order.

You must write an algorithm that runs in O(n) time and uses O(1) extra space.

##### Example 1:
```markdown
Input: n = 13
Output: [1,10,11,12,13,2,3,4,5,6,7,8,9]
```
##### Example 2:
```markdown
Input: n = 2
Output: [1,2]
```
##### Constraints:
* 1 <= n <= 5 * 10^4

### Solution:
we can imagine such a tree, out task is to traversal it with DFS, and collect numbers along the way: 1, 10, 100, ... you get it. When we encounter a number larger than n, we can return back to the previous level.
![](../../assets/images/ds/1480987290472-upload-12fc3406-aae6-484c-a653-1fa91e5f2ec5.png)
```java
class Solution {
    public List<Integer> lexicalOrder(int n) {
        List<Integer> list = new LinkedList<>();
        for(int i = 1; i <= 9; i++) dfs(i, n, list);
        return list;
    }

    public void dfs(int value, int n, List<Integer> list){
        if(value > n) return;
        list.add(value);
        for(int i = 0; i <= 9; i++){
            dfs(value * 10 + i, n, list);
        }
    }
}
```
##### Optimising unnecessary calls if number greater than target value
```java
class Solution {
    public List<Integer> lexicalOrder(int n) {
        List<Integer> result = new ArrayList<>();
        generate(result, 1, n);
        return result;
    }
    
    private void generate(List<Integer> l, int cur, int n) {
        if (cur > n) return;
        l.add(cur);
        generate(l, cur*10, n);
        if (cur%10 != 9) generate(l, cur+1, n);
    }
}
```