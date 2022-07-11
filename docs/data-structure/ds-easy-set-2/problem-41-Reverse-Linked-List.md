---
layout: default
title: Reverse Linked List
parent: Data Structure Easy Set 2
grand_parent: Data Structure
nav_order: 10
permalink: /problem-41-Reverse-Linked-List/
---
# Reverse Linked List

Given the head of a singly linked list, reverse the list, and return the reversed list.

##### Example 1:
```markdown
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```
### Solution
##### Non-recursive 
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
    public ListNode reverseList(ListNode head) {
        if(head == null) return head;
        ListNode ptr = null, qtr ;
        while(head != null){
            qtr = head;
            head = head.next;
            qtr.next = ptr;
            ptr = qtr;
        }
        return ptr;
    }
}
```
##### Recursive
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head == null) return head;
        if(head.next == null) return head;
        ListNode newNode = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return newNode;
        
    }
}
```