---
layout: default
title: Binary Tree Preorder Traversal
parent: Easy Set 1
grand_parent: DSA Easy Difficulty
nav_order: 30
permalink: /problem-31-Binary-Tree-Preorder-Traversal/
---
# Binary Tree Preorder Traversal
Given the root of a binary tree, return the preorder traversal of its nodes' values.
##### Example 1:
```markdown
Input: root = [1,null,2,3]
Output: [1,2,3]
```

##### Example 2:
```markdown
Input: root = []
Output: []
```

##### Example 3:
```markdown
Input: root = [1]
Output: [1]
```

### Solution
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<Integer>();
        return preorderTraversal(root, list);
    }
    
    public List<Integer> preorderTraversal(TreeNode head, List<Integer> list){
        if(head == null) return list;
        list.add(head.val);
        preorderTraversal(head.left,list);
        preorderTraversal(head.right,list);
        return list;
    }
}
```
# Binary Tree Postorder Traversal
##### Example 1:
```markdown
Input: root = [1,null,2,3]
Output: [3,2,1]
```
##### Example 2:
```markdown
Input: root = []
Output: []
```
### Solution
```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
     List<Integer> list = new ArrayList<Integer>();
        return postorderTraversal(root, list);
    }
    
    public List<Integer> postorderTraversal(TreeNode head, List<Integer> list){
        if(head == null) return list;
        postorderTraversal(head.left,list);
        postorderTraversal(head.right,list);
        list.add(head.val);
        return list;
    }
}
```


