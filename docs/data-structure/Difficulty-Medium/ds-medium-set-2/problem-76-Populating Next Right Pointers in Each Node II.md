---
layout: default
title: Populating Next Right Pointers in Each Node II
parent: Data Structure Medium Set 2
grand_parent: Data Structure
nav_order: 26
permalink: /problem-76-Populating Next Right Pointers in Each Node II/
---
# Populating Next Right Pointers in Each Node II

Given a binary tree

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

##### Example 1:
![](../../assets/images/ds/117_sample.png)
```markdown
Input: root = [1,2,3,4,5,null,7]
Output: [1,#,2,3,#,4,5,7,#]
Explanation: Given the above binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```
##### Example 2:
```markdown
Input: root = []
Output: []
```
##### Constraints:
* The number of nodes in the tree is in the range [0, 6000].
* -100 <= Node.val <= 100

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
            Node currNode = levelNode;
           
            while(currNode != null){
                // connecting left node
                if(currNode.left != null){
                    if(currNode.right != null){
                        currNode.left.next = currNode.right;
                    }else{
                        Node ptr = currNode.next;
                        while(ptr != null){
                            if(ptr.left != null){
                                currNode.left.next = ptr.left;
                                break;
                            }
                            if(ptr.right != null){
                                currNode.left.next = ptr.right;
                                break;
                            } 
                            ptr = ptr.next; 
                        }
                    }
                }

                // connecting right node
                if(currNode.right != null && currNode.next != null){
                    Node ptr = currNode.next;
                    while(ptr != null){
                        if(ptr.left != null){
                            currNode.right.next = ptr.left;
                            break;
                        }
                        if(ptr.right != null){
                            currNode.right.next = ptr.right;
                            break;
                        } 
                        ptr = ptr.next; 
                    }
                }
                // pointing next node in same level
                currNode = currNode.next;
            }
            // finding next level node
            while(levelNode != null && levelNode.left == null && levelNode.right == null) levelNode = levelNode.next;
            if(levelNode != null && levelNode.left != null) levelNode = levelNode.left;
            else if(levelNode != null && levelNode.right != null) levelNode = levelNode.right;
        }
        return root;
    }
}
```
