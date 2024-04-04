---
layout: default
title: Subtree of Another Tree
parent: Easy Set 4
grand_parent: DSA Easy
nav_order: 5
permalink: /problem-105-Subtree-of-Another-Tree/
---
# Subtree of Another Tree
Given the roots of two binary trees root and subRoot, return true if there is a subtree of root with the same structure and node values of subRoot and false otherwise.

A subtree of a binary tree tree is a tree that consists of a node in tree and all of this node's descendants. The tree tree could also be considered as a subtree of itself.

##### Example 1:
![](../../assets/images/ds/subtree1-tree.jpeg)
```markdown
Input: root = [3,4,5,1,2], subRoot = [4,1,2]
Output: true
```
##### Example 2:
![](../../assets/images/ds/subtree2-tree.jpeg)
```markdown
Input: root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
Output: false
```
##### Constraints:
* The number of nodes in the root tree is in the range [1, 2000].
* The number of nodes in the subRoot tree is in the range [1, 1000].
* -104 <= root.val <= 104
* -104 <= subRoot.val <= 104

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
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        Stack<TreeNode> s1 = new Stack<>();
        Stack<TreeNode> s2 = new Stack<>();
        Stack<TreeNode> s3 = new Stack<>();
        s1.push(root);
        int count = countNode(subRoot);
        System.out.println("Count: "+count);
        while(!s1.isEmpty()){
            TreeNode node = s1.pop();
            
            if(node.val == subRoot.val){
                TreeNode sub = subRoot;
                s2.clear();
                s3.clear();
                s2.push(node);
                s3.push(sub);
                int c = 0;
                while(!s3.isEmpty()){
                    TreeNode n1 = s3.pop();
                    if(s2.isEmpty()) break;
                    TreeNode n2 = s2.pop();
                    if(n1.val != n2.val) break;
                    
                    if(n1.left != null){
                        if(n2.left == null) break;
                        s3.push(n1.left);
                        s2.push(n2.left);
                    } 
                    if(n1.left == null && n2.left != null) break;
                    
                    if(n1.right != null){
                        if(n2.right == null) break;
                        s3.push(n1.right);
                        s2.push(n2.right);
                    }
                    
                    if(n1.right == null && n2.right != null) break;
                    c++;
                }
                if(c == count) return true;
            }
            if(node.left != null) s1.push(node.left);
            if(node.right != null) s1.push(node.right);
        }
        return false;
    }
    
    public int countNode(TreeNode head){
        if(head == null) return 0;
        return 1 + countNode(head.left) + countNode(head.right);
    }
}
```
#### Hash solution 
The main idea of this solution is that every subtree of root can be hashed. The general technique is called Merkle Tree Hashing.

Consider a tree with a root value of v. Recursively hash the left and right subtree (storing their hashes in a global list - in my code the ArrayList hashes). In my code, my hash combiner function is (v + L*B + R * B*B)%M.

* B is the base of the hash, M is the mod of the hash.
* L and R are the hashes of the left and right subtrees, which can be calculated recursively via DFS.
After we compute the hashes of all subtrees of root, we can check to see if any of them equal the hash of subRoot.

The time complexity is O(N) because our DFS processes each node of the tree. At each step, the actual hashing is O(1).

The space complexity is O(N) because we store the hashes of each node.
```java
class Solution {

    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        Merkle mht = new Merkle(root);
        long H = (new Merkle(subRoot)).hash();
        for (long h: mht.hashes) {
            if (h==H) return true;
        }
        return false;
    }
    
    static class Merkle {
        long B = 20051L;
        long M = 1000000007L;
        ArrayList<Long> hashes;
        public Merkle(TreeNode t) {
            hashes = new ArrayList<Long>();
            dfs(t);
        }
        
        //hash of the entire tree
        long hash() {
            return hashes.get(hashes.size()-1);
        }
        
        //left is *B, right is *B^2
        long dfs(TreeNode t) {
            long H = t.val+10004;
            if (t.left != null) {
                H += dfs(t.left)*B;
            }
            if (t.right != null) {
                H += dfs(t.right)*B*B;
            }
            H %= M;
            hashes.add(H);
            return H;
        }
    }
}
```
#### Recursive 
```java
class Solution {
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if(root == null){
            return false;
        }else if(isSameTree(root, subRoot)){
			//checking if they overlap each other or not
            return true;
        }else if(isSubtree(root.left, subRoot)){
			//checking on left child of root if subTree matches there
            return true;
        }else{
			//checking on right child of root if subTree matches there
            return isSubtree(root.right, subRoot);
        }
    }
    public boolean isSameTree(TreeNode root, TreeNode subRoot){
        if(root == null || subRoot == null){
            return root == null && subRoot == null;
        }else if(root.val == subRoot.val){ //if val is same at both nodes, then only we will check forward
            if(isSameTree(root.left, subRoot.left) == false){
				//now checking left part of both of them
                return false;
            }
			//now checking right part of both of them
            return isSameTree(root.right, subRoot.right);
        }else{
            return false;
        }
    }
}
```




