---
layout: default
title: Reorder List
parent: Medium Set 2
grand_parent: DSA Medium Difficulty
nav_order: 23
permalink: /problem-73-Reorder List/
---
# Reorder List
You are given the head of a singly linked-list. The list can be represented as:

L0 → L1 → … → Ln - 1 → Ln
Reorder the list to be on the following form:

L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
You may not modify the values in the list's nodes. Only nodes themselves may be changed.

##### Example 1:
![](../../assets/images/ds/reorder1linked-list.jpeg)
```markdown
Input: head = [1,2,3,4]
Output: [1,4,2,3]
```
##### Example 2:
![](../../assets/images/ds/reorder2-linked-list.jpeg)
```markdown
Input: head = [1,2,3,4,5]
Output: [1,5,2,4,3]
```
##### Constraints:
* The number of nodes in the list is in the range [1, 5 * 10^4].
* 1 <= Node.val <= 1000

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
    public void reorderList(ListNode head) {
        if(head == null || head.next == null) return;
        // finding middle of the list  1->2->3->4->5 => 1->2  3->4->5
        ListNode slow = head, fast = head, prev = head;
        while(fast != null && fast.next != null){
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        prev.next = null;
        // reverse the middle list 1->2 5->4->3
        ListNode revList = null, ptr, qtr;
        while(slow != null){
           ptr = slow.next;
           slow.next = revList;
           revList = slow;
           slow = ptr;
        }
        // reoder the list
        ptr = head;
        while(ptr.next != null){
            qtr = revList.next;
            revList.next = ptr.next;
            ptr.next = revList;
            slow = ptr.next;
            ptr = ptr.next.next;
            revList = qtr;
        }
        ptr.next = revList;
    }
}
```