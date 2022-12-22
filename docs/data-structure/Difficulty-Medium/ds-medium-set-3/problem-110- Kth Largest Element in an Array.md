---
layout: default
title: Kth Largest Element in an Array
parent: Data Structure Medium Set 3
grand_parent: Data Structure
nav_order: 10
permalink: /problem-110-Kth Largest Element in an Arrays/
---
#  Kth Largest Element in an Array
Given an integer array nums and an integer k, return the kth largest element in the array.

Note that it is the kth largest element in the sorted order, not the kth distinct element.

You must solve it in O(n) time complexity.

##### Example 1:
```markdown
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5
```
##### Example 2:
```markdown
Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
```
##### Constraints:
* 1 <= k <= nums.length <= 10^5
* -10^4 <= nums[i] <= 10^4

### Solution:
##### Using Quick select, O(n)
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        // implementing using quick select algorithm. avarage case time complexity O(n), wrost case O(n^2).

        // calculating target index
        k = nums.length - k;
        
        // initializing target list boundaries
        int lower = 0;
        int upper = nums.length - 1;

        while(lower < upper){
            // finding pivote element index
            int pivote  = partitionList(nums, lower, upper);
            if(pivote < k){
                lower = pivote + 1;
            }else if(pivote > k){
                upper = pivote - 1;
            }else return nums[pivote];
        } 

        return nums[k];
    }

    private int partitionList(int[] nums, int start, int end){
        int pivote = start;

        while(start <= end){
            while(start <= end && nums[start] <= nums[pivote])start ++;
            while(start <= end && nums[end] > nums[pivote]) end --;
            if(start > end) break;
            swap(nums, start, end);
        }
        swap(nums, pivote, end);
        return end;
    }

    public void swap(int[] nums, int i, int j){
        int temp = nums[j];
        nums[j] = nums[i];
        nums[i] = temp;
    }
}
```

##### Using Max Heap
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>(new Comparator<Integer>(){
            public int compare(Integer a, Integer b){
                return b.compareTo(a);
            }
        });

        for(int n : nums) pq.offer(n);
        for(int i = 1; i < k; i++) pq.poll();

        return pq.peek();
    }
}
```