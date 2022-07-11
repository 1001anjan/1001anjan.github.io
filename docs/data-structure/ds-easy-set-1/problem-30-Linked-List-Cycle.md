---
layout: default
title: Linked List Cycle
parent: Data Structure Easy Set 1
grand_parent: Data Structure
nav_order: 30
permalink: /problem-30-Linked-List-Cycle/
---
# Linked List Cycle

Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.

##### Example 1:
![](../../assets/images/ds/circularlinkedlist.png)
```markdown
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
```
##### Constraints:
* The number of the nodes in the list is in the range [0, 104].
* -105 <= Node.val <= 105
* pos is -1 or a valid index in the linked-list.

### Solution: 
##### Using extra memory
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head == null) return false;
        Set<ListNode> set = new HashSet<ListNode>();
        while(head != null){
            if(set.contains(head)) {
                return true;
            }            
            set.add(head);
            head = head.next;

        }
        return false;
    }
}
```
#### Using constant memory
```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode fast = head;
        ListNode last = head;
        
        while(fast != null && fast.next != null){
            fast = fast.next.next;
            last = last.next;
            if(fast == last){
                return true;
            }
        }
        return false;
    }
}
```

