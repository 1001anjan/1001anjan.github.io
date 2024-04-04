---
layout: default
title: Populating Next Right Pointers in Each Node
parent: Medium Set 2
grand_parent: DSA Medium
nav_order: 25
permalink: /problem-75-Populating Next Right Pointers in Each Node/
---
# Populating Next Right Pointers in Each Node
You are given a perfect binary tree where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:
```markdown
struct Node {
int val;
Node *left;
Node *right;
Node *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.
![](../../assets/images/ds/116_sample.png)
##### Example 1:
```markdown
Input: root = [1,2,3,4,5,6,7]
Output: [1,#,2,3,#,4,5,6,7,#]
Explanation: Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```
#####Example 2:
```markdown
Input: root = []
Output: []
```
##### Constraints:
* The number of nodes in the tree is in the range [0, 212 - 1].
* -1000 <= Node.val <= 1000

##### Follow-up:
* You may only use constant extra space.
* The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.

### Solution:
```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node next;

    public Node() {}
    
    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, Node _left, Node _right, Node _next) {
        val = _val;
        left = _left;
        right = _right;
        next = _next;
    }
};
*/

class Solution {
    public Node connect(Node root) {
        Node levelNode = root;
        
        while(levelNode != null){
            Node ptr = levelNode;
            while(ptr != null){
                if(ptr.left != null) ptr.left.next = ptr.right;
                if(ptr.right != null && ptr.next != null) ptr.right.next = ptr.next.left;

                ptr = ptr.next;
            }
            levelNode = levelNode.left;
        }

        return root;
    }
}
```