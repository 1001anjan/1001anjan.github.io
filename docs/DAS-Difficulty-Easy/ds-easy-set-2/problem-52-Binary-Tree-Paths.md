---
layout: default
title: Binary Tree Paths
parent: Easy Set 2
grand_parent: DSA Easy Difficulty
nav_order: 21
permalink: /problem-52-Binary-Tree-Paths/
---
# Binary Tree Paths

Given the root of a binary tree, return all root-to-leaf paths in any order.

A leaf is a node with no children.

##### Example 1:
![](../../assets/images/ds/paths-tree.jpeg)
```markdown
Input: root = [1,2,3,null,5]
Output: ["1->2->5","1->3"]
```
##### Constraints:
* The number of nodes in the tree is in the range [1, 100].
* -100 <= Node.val <= 100

### Solution
##### Non-recursive
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

class NodeMap{
    public TreeNode head;
    public StringBuilder sb;
    NodeMap(TreeNode head, String val){
        sb = new StringBuilder(val);
        this.head = head;
    }
}

class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> list = new ArrayList<String>();
       Stack<NodeMap> stack = new Stack<NodeMap>();
        stack.push(new NodeMap(root, String.valueOf(root.val)));
        NodeMap nodeMap;
        while(!stack.isEmpty()){
            nodeMap = stack.pop();
            if(nodeMap.head.left == null && nodeMap.head.right == null){
                list.add(nodeMap.sb.toString().substring(0,nodeMap.sb.length()));
            }
            if(nodeMap.head.right != null){
                stack.push(new NodeMap(nodeMap.head.right, nodeMap.sb.toString()+"->"+String.valueOf(nodeMap.head.right.val)));
            }
            if(nodeMap.head.left != null){
                stack.push(new NodeMap(nodeMap.head.left, nodeMap.sb.toString()+"->"+String.valueOf(nodeMap.head.left.val)));
            } 
        }
      return list;             
    }
}
```
##### Recursive
```java
class Solution {
    List<String> res = new ArrayList<>();
    
    public List<String> binaryTreePaths(TreeNode root) {
        helper(root, new StringBuilder());
        return res;
    }
    
    public void helper(TreeNode node, StringBuilder sb) {
        if (node == null) return;
        int len = sb.length();
        sb.append(node.val);
        
        if (node.left == null && node.right == null) {
            res.add(sb.toString());
        } else {
            sb.append("->");
            helper(node.left, sb);
            helper(node.right, sb);
        }
        // deleting the extra characters we added
        sb.setLength(len);
    }
}
```

