---
layout: default
title: Reverse Linked List II
parent: Medium Set 2
grand_parent: DSA Medium
nav_order: 2
permalink: /problem-52-Reverse Linked List II/
---
# Reverse Linked List II
Given the head of a singly linked list and two integers left and right where left <= right, reverse the nodes of the list from position left to position right, and return the reversed list.

##### Example 1:
![](../../assets/images/ds/rev2ex2.jpeg)

```markdown
Input: head = [1,2,3,4,5], left = 2, right = 4
Output: [1,4,3,2,5]
```
##### Example 2:
```markdown
Input: head = [5], left = 1, right = 1
Output: [5]
```
##### Constraints:
* The number of nodes in the list is n.
* 1 <= n <= 500
* -500 <= Node.val <= 500
* 1 <= left <= right <= n

Follow up: Could you do it in one pass?

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
    public ListNode reverseBetween(ListNode head, int left, int right) {

        ListNode dummyHead = new ListNode(1000), ptr, lptr, rptr;
        Stack<ListNode> stack = new Stack<>();

        dummyHead.next = head;
        ptr = dummyHead;

        // searching left node
        int count = 1;
        while(ptr.next != null && count++ != left) ptr = ptr.next;
        if(ptr.next == null) return head;
        
        lptr = ptr;
        ptr = ptr.next;
       
        // searching right node
        while(ptr != null && count++ != right + 1){
            stack.push(ptr);
            ptr = ptr.next;
        } 
        if(ptr == null) return head;
        stack.push(ptr);
        rptr = ptr.next;
        
        if(stack.size() == 1) return head;

        while(!stack.isEmpty()){
            ptr = stack.pop();
            lptr.next = ptr;
            lptr = ptr;
        }
        lptr.next = rptr;

        return dummyHead.next;
        
    }
}
```

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
    public ListNode reverseBetween(ListNode head, int left, int right) {

        ListNode dummyHead = new ListNode(1000), ptr, lptr, rptr, rev = null;
        
        dummyHead.next = head;
        ptr = dummyHead;

        for(int i = 0; i < left - 1; i++, ptr = ptr.next);

        lptr = ptr;
        ptr = ptr.next;
        rptr = ptr;

        for(int i = left; i <= right; i++){
            ListNode qtr = ptr;
            ptr = ptr.next;
            qtr.next = rev;
            rev = qtr;
        }
        lptr.next = rev;
        rptr.next = ptr;
        return dummyHead.next;
    }
}
```
