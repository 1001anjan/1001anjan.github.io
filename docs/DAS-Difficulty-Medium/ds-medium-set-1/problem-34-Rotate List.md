---
layout: default
title: Rotate List
parent: Medium Set 1
grand_parent: DSA Medium Difficulty
nav_order: 34
permalink: /problem-34-Rotate List/
---
# Rotate List
Given the head of a linked list, rotate the list to the right by k places.
##### Example 1:
![](../../assets/images/ds/rotate1.jpeg)
```markdown
Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]
```
##### Example 2:
![](../../assets/images/ds/roate2.jpeg)
```markdown
Input: head = [0,1,2], k = 4
Output: [2,0,1]
```
##### Constraints:
* The number of nodes in the list is in the range [0, 500].
* -100 <= Node.val <= 100
* 0 <= k <= 2 * 10^9

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
    public ListNode rotateRight(ListNode head, int k) {
        if(head == null || k ==0 || head.next == null) return head;
        int len = 1;
        ListNode ptr;
        ptr = head;
        while(ptr.next != null){
            len++;
            ptr = ptr.next;
        }
        int t = k % len;
        if(t == 0) return head;
        ListNode slow, fast;
        slow = fast = head;
        for(int i = 0; i < t && fast.next != null; i++, fast = fast.next);
        while(fast.next != null){
            slow = slow.next;
            fast = fast.next;
        }
        ptr = slow.next;
        slow.next = null;
        fast.next = head;
        head = ptr;

        return head;
    }
}
```