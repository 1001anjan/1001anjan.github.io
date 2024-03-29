---
layout: default
title: Insertion Sort List
parent: Medium Set 2
grand_parent: DSA Medium
nav_order: 15
permalink: /problem-65-Insertion Sort List/
---
# Insertion Sort List
Given the head of a singly linked list, sort the list using insertion sort, and return the sorted list's head.

The steps of the insertion sort algorithm:

Insertion sort iterates, consuming one input element each repetition and growing a sorted output list.
At each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list and inserts it there.
It repeats until no input elements remain.
The following is a graphical example of the insertion sort algorithm. The partially sorted list (black) initially contains only the first element in the list. One element (red) is removed from the input data and inserted in-place into the sorted list with each iteration.
![](../../assets/images/ds/Insertion-sort-example-300px.gif)
##### Example 1:
![](../../assets/images/ds/sort1linked-list.jpeg)
```markdown
Input: head = [4,2,1,3]
Output: [1,2,3,4]
```
##### Example 2:
![](../../assets/images/ds/sort2linked-list.jpeg)
```markdown
Input: head = [-1,5,3,4,0]
Output: [-1,0,3,4,5]
```
##### Constraints:
* The number of nodes in the list is in the range [1, 5000].
* -5000 <= Node.val <= 5000

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
    public ListNode insertionSortList(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode ptr = head, sortedList = null, qtr;
        while(ptr != null){
            qtr = ptr;
            ptr = ptr.next;
            sortedList = insertSortedList(sortedList, qtr);
        } 
        return sortedList;
    }

    public ListNode insertSortedList(ListNode list, ListNode node){
        if(list == null){
            list = node;
            list.next = null;
            return list;
        }
        // inserting as first node
        if(list.val >= node.val){
            node.next = list;
            list = node;
            return list;
        }
        // inserting to middle
        ListNode ptr = list;
        while(ptr.next != null){
            if(ptr.next.val > node.val){
                node.next = ptr.next;
                ptr.next = node;
                return list;
            }
            ptr = ptr.next;
        }
        // inserting as end node
        ptr.next = node;
        node.next = null;
        return list;
    }
}
```