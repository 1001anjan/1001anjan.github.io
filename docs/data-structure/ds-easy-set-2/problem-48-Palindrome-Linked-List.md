---
layout: default
title: Palindrome Linked List
parent: Data Structure Easy Set 2
grand_parent: Data Structure
nav_order: 17
permalink: /problem-48-Palindrome-Linked-List/
---
# Palindrome Linked List

Given the head of a singly linked list, return true if it is a palindrome.

##### Example 1:
```markdown
Input: head = [1,2,2,1]
Output: true
```
##### Example 2:
```markdown
Input: head = [1,2]
Output: false
```
##### Constraints:
* The number of nodes in the list is in the range [1, 105].
* 0 <= Node.val <= 9

### Solution
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
    public boolean isPalindrome(ListNode head) {
        ListNode slow, fast;
        slow = fast = head;
        
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        if(fast != null) slow = slow.next;
        slow = reverseList(slow);
        return compareList(head, slow);
    }
    
    public ListNode reverseList(ListNode head){
        ListNode ptr = null, qtr;
        while(head != null){
            qtr = ptr;
            ptr = head;
            head = head.next;
            ptr.next = qtr;
        }
        return ptr;
    }
    
    public boolean compareList(ListNode l1, ListNode l2){
        while(l1 != null && l2 != null){
            if(l1.val != l2.val) return false;
            l1 = l1.next;
            l2 = l2.next;
        }
     //   if(l1 != null || l2 != null) return false;
        return true;
    }
}
```