---
layout: default
title: Convert Sorted List to Binary Search Tree
parent: Medium Set 2
grand_parent: DSA Medium
nav_order: 9
permalink: /problem-59-Convert Sorted List to Binary Search Tree/
---
# Convert Sorted List to Binary Search Tree
Given the head of a singly linked list where elements are sorted in ascending order, convert it to a height-balanced binary search tree.

##### Example 1:
![](../../assets/images/ds/linked.jpeg)
```markdown
Input: head = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: One possible answer is [0,-3,9,-10,null,5], which represents the shown height balanced BST.
```
##### Example 2:
```markdown
Input: head = []
Output: []
```
##### Constraints:
* The number of nodes in head is in the range [0, 2 * 104].
* -10^5 <= Node.val <= 10^5

### Solution:
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
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
    public TreeNode sortedListToBST(ListNode head) {
        return constractBST(head);
    }

    public TreeNode constractBST(ListNode head){
        if(head == null) return null;
        if(head.next == null) return new TreeNode(head.val);
        ListNode slow, fast, pre;
        slow = fast = pre = head;
        while(fast != null && fast.next != null){
            pre = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        pre.next = null;
        TreeNode root = new TreeNode(slow.val);
        root.left = constractBST(head);
        root.right = constractBST(slow.next);

        return root;
    }
}
```