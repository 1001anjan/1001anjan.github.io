---
layout: default
title: Maximize Sum Of Array After K Negations
parent: Easy Set 6
grand_parent: DSA Easy
nav_order: 1
permalink: /problem-161-Maximize-Sum-Of-Array-After-K-Negations/
---
# Maximize Sum Of Array After K Negations

Given an integer array nums and an integer k, modify the array in the following way:

* choose an index i and replace nums[i] with -nums[i].
You should apply this process exactly k times. You may choose the same index i multiple times.

Return the largest possible sum of the array after modifying it in this way.

##### Example 1:
```markdown
Input: nums = [4,2,3], k = 1
Output: 5
Explanation: Choose index 1 and nums becomes [4,-2,3].
```
##### Example 2:
```markdown
Input: nums = [3,-1,0,2], k = 3
Output: 6
Explanation: Choose indices (1, 2, 2) and nums becomes [3,1,0,2].
```
##### Example 3:
```markdown
Input: nums = [2,-3,-1,5,-4], k = 2
Output: 13
Explanation: Choose indices (1, 4) and nums becomes [2,3,-1,5,4].
```
##### Constraints:
* 1 <= nums.length <= 104
* -100 <= nums[i] <= 100
* 1 <= k <= 104

### Solution:
```java
class Solution {
    public int largestSumAfterKNegations(int[] nums, int k) {
        Arrays.sort(nums);
        int i = 0;
        // checking for negetive elements
        while(i<k && i<nums.length && nums[i]<0){
            nums[i] *=-1;
            i++;
        }
        if(i == nums.length){
            if(k%2 == 0) nums[nums.length-1] *=-1;
        }else{
           k = k - i;
        // checking if positive element 
            if(i<nums.length && nums[i] > 0){
            // check if we have previous postive element
                if(i>0 && nums[i-1]>0 && nums[i-1]<nums[i] && k%2 == 1) nums[i-1] *= -1;
                else if(k%2 == 1) nums[i] *= -1;
            } 
        }                                   
        
        int sum = 0;
        for(int n : nums) sum +=n; 
        return sum;
    }
}
```
#### Using mean heap but slower than previous
```java
class Solution {
public int largestSumAfterKNegations(int[] nums, int k) {

    PriorityQueue<Integer>pq=new PriorityQueue<>((a,b)->a-b);
    
    int sum=0;
    for(int i:nums){
        pq.add(i);
    }
    
    while(k>0){
        int x=pq.poll();
        pq.add(-x);
        k--;
    }
    
    while(pq.size()>0){
        sum+=pq.poll();
    }
    return sum;
}
}

```

