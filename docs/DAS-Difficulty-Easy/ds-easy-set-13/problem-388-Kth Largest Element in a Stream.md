---
layout: default
title: Kth Largest Element in a Stream
parent: Easy Set 13
grand_parent: DSA Easy
nav_order: 18
permalink: /problem-388-Kth Largest Element in a Stream/
---
# Kth Largest Element in a Stream
Design a class to find the kth largest element in a stream. Note that it is the kth largest element in the sorted order, not the kth distinct element.

Implement KthLargest class:

KthLargest(int k, int[] nums) Initializes the object with the integer k and the stream of integers nums.
int add(int val) Appends the integer val to the stream and returns the element representing the kth largest element in the stream.

##### Example 1:
```markdown
Input
["KthLargest", "add", "add", "add", "add", "add"]
[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]
Output
[null, 4, 5, 5, 8, 8]

Explanation
KthLargest kthLargest = new KthLargest(3, [4, 5, 8, 2]);
kthLargest.add(3);   // return 4
kthLargest.add(5);   // return 5
kthLargest.add(10);  // return 5
kthLargest.add(9);   // return 8
kthLargest.add(4);   // return 8
```
##### Constraints:
* 1 <= k <= 104
* 0 <= nums.length <= 104
* -104 <= nums[i] <= 104
* -104 <= val <= 104
* At most 104 calls will be made to add.
* It is guaranteed that there will be at least k elements in the array when you search for the kth element.

### Solution:
```java
class KthLargest {
    private int k;
    private PriorityQueue<Integer> heap;

    public KthLargest(int k, int[] nums) {
        this.k = k;
        heap = new PriorityQueue<>();
        for(int n : nums) heap.offer(n);
        while(heap.size() > k) heap.poll();
    }
    
    public int add(int val) {
        heap.offer(val);
        if (heap.size() > k) {
            heap.poll();
        }
        return heap.peek();
    }
}

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest obj = new KthLargest(k, nums);
 * int param_1 = obj.add(val);
 */
```