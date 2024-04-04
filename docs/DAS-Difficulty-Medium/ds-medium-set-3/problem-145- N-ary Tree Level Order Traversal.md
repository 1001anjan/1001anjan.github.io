---
layout: default
title: N-ary Tree Level Order Traversal
parent: Medium Set 3
grand_parent: DSA Medium
nav_order: 45
permalink: /problem-145-N-ary Tree Level Order Traversal/
---
#  N-ary Tree Level Order Traversal
Given an n-ary tree, return the level order traversal of its nodes' values.

Nary-Tree input serialization is represented in their level order traversal, each group of children is separated by the null value (See examples).

##### Example 1:
![](../../assets/images/ds/narytreeexample.png)
```markdown
Input: root = [1,null,3,2,4,null,5,6]
Output: [[1],[3,2,4],[5,6]]
```
##### Example 2:
![](../../assets/images/ds/sample_4_964.png)
```markdown
Input: root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
Output: [[1],[2,3,4,5],[6,7,8,9,10],[11,12,13],[14]]
```
##### Constraints:
* The height of the n-ary tree is less than or equal to 1000
* The total number of nodes is between [0, 10^4]

### Solution:
```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/


class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> list = new LinkedList<>();
        if(root == null) return list;
        Queue<Node> q = new LinkedList<>();
        q.offer(root);
        while(!q.isEmpty()){
            Queue<Node> q1 = new LinkedList<>();
            List<Integer> l = new LinkedList<>();
            while(!q.isEmpty()){
                Node n = q.poll();
                l.add(n.val);
                for(Node ch : n.children) q1.offer(ch);
            }

            list.add(l);
            q = q1;
        }
        return list;
    }
}
```
