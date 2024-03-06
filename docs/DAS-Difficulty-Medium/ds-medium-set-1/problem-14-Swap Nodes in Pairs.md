---
layout: default
title: Swap Nodes in Pairs
parent: Medium Set 1
grand_parent: DSA Medium
nav_order: 14
permalink: /problem-14-Swap Nodes in Pairs/
---
# Swap Nodes in Pairs
Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)


##### Example 1:
![](../../assets/images/ds/swap_ex1.jpeg)
```markdown
Input: head = [1,2,3,4]
Output: [2,1,4,3]
```
##### Example 2:
```markdown
Input: head = []
Output: []
```
##### Example 3:
```markdown
Input: head = [1]
Output: [1]
```
##### Constraints:
* The number of nodes in the list is in the range [0, 100].
* 0 <= Node.val <= 100

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
class Solution {
    public ListNode swapPairs(ListNode head) {
        // corner cases
        if(head == null || head.next == null ) return head;
        // swapping head
        ListNode ptr, qtr;
        ptr = head;
        qtr = head.next;

        head = qtr;
        ptr.next = qtr.next;
        qtr.next = ptr;

        // swapping remaining node
        ptr = head.next;
        if(ptr.next == null) return head;
        ListNode mtr = ptr.next;
        qtr = mtr.next;
        while(qtr != null){
            ptr.next = qtr;
            mtr.next = qtr.next;
            qtr.next = mtr;

            ptr = mtr;
            if(ptr.next == null) return head;
            mtr = ptr.next;
            if(mtr == null) return head;
            qtr = mtr.next;

        }

        return head;
    }
}
```