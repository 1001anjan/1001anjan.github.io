---
layout: default
title: Binary Tree Level Order Traversal
parent: Data Structure Medium Set 2
grand_parent: Data Structure
nav_order: 5
permalink: /problem-55-Binary Tree Level Order Traversal/
---
# Binary Tree Level Order Traversal
Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

##### Example 1:
![](../../assets/images/ds/tree11212.jpeg)
```markdown
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
```
##### Example 2:
```markdown
Input: root = [1]
Output: [[1]]
```
##### Example 3:
```markdown
Input: root = []
Output: []
```
##### Constraints:
* The number of nodes in the tree is in the range [0, 2000].
* -1000 <= Node.val <= 1000

### Solution:
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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ans = new ArrayList<>();
        if(root == null) return ans;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        int count = 1;

        while(!queue.isEmpty()){
            Queue<TreeNode> temp = new LinkedList<>();
            List<Integer> list = new ArrayList<>();
            int c = 0;

            while(count > 0){
                TreeNode n = queue.remove();
                list.add(n.val);
                if(n.left != null){
                    c++;
                    temp.offer(n.left);
                }
                if(n.right != null){
                    c++;
                    temp.offer(n.right);
                }
                count--;
            }

            ans.add(list);
            count = c;
            queue = temp;
        }

        return ans;
    }
}
```
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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ans = new ArrayList<>();
        processLevelOrder(root, 0, ans);
        return ans;
    }

    public void processLevelOrder(TreeNode root, int level, List<List<Integer>> ans){
        if(root == null) return;
        if(level == ans.size()){
            ans.add(new ArrayList<>());
        }
        ans.get(level).add(root.val);
        processLevelOrder(root.left, level + 1, ans);
        processLevelOrder(root.right, level + 1, ans);
    }
}
```
