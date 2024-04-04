---
layout: default
title: Wiggle Sort II
parent: Medium Set 3
grand_parent: DSA Medium
nav_order: 27
permalink: /problem-127-Wiggle Sort II/
---
# Wiggle Sort II
Given an integer array nums, reorder it such that nums[0] < nums[1] > nums[2] < nums[3]....

You may assume the input array always has a valid answer.

##### Example 1:
```markdown
Input: nums = [1,5,1,1,6,4]
Output: [1,6,1,5,1,4]
Explanation: [1,4,1,5,1,6] is also accepted.
```
##### Example 2:
```markdown
Input: nums = [1,3,2,2,3,1]
Output: [2,3,1,3,1,2]
```
##### Constraints:
* 1 <= nums.length <= 5 * 10^4
* 0 <= nums[i] <= 5000
* It is guaranteed that there will be an answer for the given input nums.

* Follow Up: Can you do it in O(n) time and/or in-place with O(1) extra space?

### Solution:
```java
class Solution {
    public void wiggleSort(int[] nums) {

        // base condition
        if(nums.length < 2) return;

        // median index
        int k = nums.length / 2;

        // find median element
        int median = findMedianElement(nums, 0, nums.length - 1, k);

        // put odd position with greater than median number
        int odd = 1;
        for(int i = k; i < nums.length; i++){
            if(nums[i] > median){
                swap(nums, odd, i);
                odd += 2;
            }
        }

         while(odd < nums.length && nums[odd] == median) odd += 2;
        // it's possible that odd positions have not been perfectly filled by elements larger than median.
        // thus we need some elements equal to median
        // put elements equal to median on odd position first, then on even position 0, 2, 4 ...
        int even = 0;
        for(int i = 0; i< nums.length; i += 2) {
            if(nums[i] == median) {
                if(odd < nums.length) {
                    swap(nums, i, odd);
                    odd += 2;
                    while(odd < nums.length && nums[odd] == median) odd += 2;
                } else {
                    swap(nums, i, even);
                    even += 2;
                }
            }
        }
        
    }

    public int findMedianElement(int[] nums, int start, int end, int k){
        int p = partition(nums, start, end);
        if(p == k) return nums[k];
        if(p > k) return findMedianElement(nums, start, p - 1, k);
        else return findMedianElement(nums, p + 1, end, k);
    }

    public int partition(int[] nums, int start, int end){
        int pivote = start;
        while(start <= end){
            while(start <= end && nums[start] <= nums[pivote]) start ++;
            while(start <= end && nums[pivote] < nums[end]) end --;
            if(start > end) break;
            swap(nums, start, end);
        }

        swap(nums, pivote, end);
        return end;
    }

    public void swap(int[] nums, int i, int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```