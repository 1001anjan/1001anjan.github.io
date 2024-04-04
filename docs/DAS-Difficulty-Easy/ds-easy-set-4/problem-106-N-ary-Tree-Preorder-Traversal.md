---
layout: default
title: N-ary Tree Preorder Traversal
parent: Easy Set 4
grand_parent: DSA Easy
nav_order: 6
permalink: /problem-106-N-ary-Tree-Preorder-Traversal/
---
# N-ary Tree Preorder Traversal

Given the root of an n-ary tree, return the preorder traversal of its nodes' values.

Nary-Tree input serialization is represented in their level order traversal. Each group of children is separated by the null value (See examples)

##### Example 1:
![](../../assets/images/ds/narytreeexample.png)
```markdown
Input: root = [1,null,3,2,4,null,5,6]
Output: [1,3,5,6,2,4]
```
##### Constraints:
* The number of nodes in the tree is in the range [0, 104].
* 0 <= Node.val <= 104
* The height of the n-ary tree is less than or equal to 1000.

### Solution
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
    List<Integer> list = new ArrayList<>();
    public List<Integer> preorder(Node root) {
        if(root == null) return list;
        list.add(root.val);
        for(Node n : root.children)
            preorder(n);
        return list;
    }
}
```


