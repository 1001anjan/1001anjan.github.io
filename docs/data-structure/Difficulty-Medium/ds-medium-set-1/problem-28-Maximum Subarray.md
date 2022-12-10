---
layout: default
title: Maximum Subarray
parent: Data Structure Medium Set 1
grand_parent: Data Structure
nav_order: 28
permalink: /problem-28-Maximum Subarray/
---
# Maximum Subarray
Given an integer array nums, find the subarray which has the largest sum and return its sum.

##### Example 1:
```markdown
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```
##### Example 2:
```markdown
Input: nums = [1]
Output: 1
```
##### Example 3:
```markdown
Input: nums = [5,4,-1,7,8]
Output: 23
```
##### Constraints:
* 1 <= nums.length <= 10^5
* -10^4 <= nums[i] <= 10^4


Follow up: If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

### Solution: 
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int maxSum = nums[0];
        int currSum = nums[0];

        for(int i = 1; i < nums.length; i++){
            if(currSum + nums[i] < nums[i]){
                currSum = nums[i];
            }else{
                currSum += nums[i];
            }
            maxSum = Math.max(maxSum,currSum);
        }
        return Math.max(maxSum,currSum);
    }
}
```
```java
class Solution {
    public int maxSubArray(int[] nums) {
        return divideAndConquer(nums, 0, nums.length - 1);
    }
    public int divideAndConquer(int[] arr, int l, int u){
        if( l > u) return Integer.MIN_VALUE;
        if(l == u) return arr[l];
        int m = (l + u)/2;
        /* Return maximum of following three
        possible cases:
        a) Maximum subarray sum in left half
        b) Maximum subarray sum in right half
        c) Maximum subarray sum such that the
        subarray crosses the midpoint */

        return Math.max(Math.max(divideAndConquer(arr, l, m - 1), divideAndConquer(arr, m + 1, u)),
                maximumCrossing(arr, l, m, u));
    }

    public int maximumCrossing(int[] arr, int l, int m, int u){
        int sum = 0;
        int leftSum = Integer.MIN_VALUE;
        for(int i = m; i >= l; i--){
            sum += arr[i];
            if(sum > leftSum) leftSum = sum;
        }

        sum = 0;
        int rightSum = Integer.MIN_VALUE;
        for(int i = m; i <= u; i++){
            sum += arr[i];
            if(sum > rightSum) rightSum = sum;
        }

        return Math.max(leftSum + rightSum - arr[m], Math.max(leftSum, rightSum));
    }
}
```