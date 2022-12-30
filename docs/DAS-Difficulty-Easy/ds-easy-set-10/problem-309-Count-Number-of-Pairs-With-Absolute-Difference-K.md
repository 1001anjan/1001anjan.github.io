---
layout: default
title: Count Number of Pairs With Absolute Difference K
parent: Easy Set 10
grand_parent: DSA Easy Difficulty
nav_order: 29
permalink: /problem-309-Count-Number-of-Pairs-With-Absolute-Difference-K/
---
# Count Number of Pairs With Absolute Difference K
Given an integer array nums and an integer k, return the number of pairs (i, j) where i < j such that |nums[i] - nums[j]| == k.

The value of |x| is defined as:

* x if x >= 0.
* -x if x < 0.

##### Example 1:
```markdown
Input: nums = [1,2,2,1], k = 1
Output: 4
Explanation: The pairs with an absolute difference of 1 are:
- [1,2,2,1]
- [1,2,2,1]
- [1,2,2,1]
- [1,2,2,1]
```
##### Example 2:
```markdown
Input: nums = [1,3], k = 3
Output: 0
Explanation: There are no pairs with an absolute difference of 3.
```
##### Example 3:
```markdown
Input: nums = [3,2,1,5,4], k = 2
Output: 3
Explanation: The pairs with an absolute difference of 2 are:
- [3,2,1,5,4]
- [3,2,1,5,4]
- [3,2,1,5,4]
```
##### Constraints:
* 1 <= nums.length <= 200
* 1 <= nums[i] <= 100
* 1 <= k <= 99

### Solution: O(n) complexity with constant space
```java
class Solution {
    public int countKDifference(int[] nums, int k) {
        int i , j , max = 0 , pairs = 0 ;
        int[] count = new int[101] ;
        for( i = 0 ; i < nums.length ; i++ ){
            count[nums[i]]++ ;
            if( nums[i] > max ){
                max = nums[i] ;
            }
        }
        for( i = 1 , j = i + k ; j <= max ; i++ , j++ ){
            if( count[i] > 0 && count[j] > 0 ){
                pairs += count[i] * count[j] ;    
            }            
        }
        return pairs ;
    }
}
```
##### O(n^2 complexity)
```java
class Solution {
    public int countKDifference(int[] nums, int k) {
        int c = 0;
        Arrays.sort(nums);
        for(int i = 0; i < nums.length - 1; i++){
            for(int j = i + 1; j < nums.length; j++){
                int d = nums[j] - nums[i];
                if(d == k) c++;
                else if(d > k) break;
            }
        }
        return c;
    }
}
```