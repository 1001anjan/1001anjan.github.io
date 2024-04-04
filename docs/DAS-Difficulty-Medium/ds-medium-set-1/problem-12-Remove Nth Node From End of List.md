---
layout: default
title: Remove Nth Node From End of List
parent: Medium Set 1
grand_parent: DSA Medium
nav_order: 12
permalink: /problem-12-Remove Nth Node From End of List/
---
# Remove Nth Node From End of List
Given the head of a linked list, remove the nth node from the end of the list and return its head.

![](../../assets/images/ds/remove_ex1.jpeg)
##### Example 1:
```markdown
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```
##### Example 2:
```markdown
Input: head = [1], n = 1
Output: []
```
##### Example 3:
```markdown
Input: head = [1,2], n = 1
Output: [1]
```
##### Constraints:
* The number of nodes in the list is sz.
* 1 <= sz <= 30
* 0 <= Node.val <= 100
* 1 <= n <= sz


Follow up: Could you do this in one pass?

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode ptr, qtr;
        // Corner cases
        if(head.next == null) return null;
        // Since n >=1
        ptr = qtr = head;
        while(n > 0){
            qtr = qtr.next;
            n --;
        }
        // Traversing to the end node
        while(qtr != null && qtr.next != null){
            ptr = ptr.next;
            qtr = qtr.next;
        }
        if(qtr == null){
            ptr = head.next;
            head = null;
            return ptr;

        } 
        // deleting node
        qtr = ptr.next;
        ptr.next = qtr.next;

        return head;
    }
}
```