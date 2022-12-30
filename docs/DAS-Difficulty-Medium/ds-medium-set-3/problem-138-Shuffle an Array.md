---
layout: default
title: Shuffle an Array
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 38
permalink: /problem-138-Shuffle an Array/
---
# Shuffle an Array
Given an integer array nums, design an algorithm to randomly shuffle the array. All permutations of the array should be equally likely as a result of the shuffling.

Implement the Solution class:

* Solution(int[] nums) Initializes the object with the integer array nums.
* int[] reset() Resets the array to its original configuration and returns it.
* int[] shuffle() Returns a random shuffling of the array.

##### Example 1:
```markdown
Input
["Solution", "shuffle", "reset", "shuffle"]
[[[1, 2, 3]], [], [], []]
Output
[null, [3, 1, 2], [1, 2, 3], [1, 3, 2]]

Explanation
Solution solution = new Solution([1, 2, 3]);
solution.shuffle();    // Shuffle the array [1,2,3] and return its result.
// Any permutation of [1,2,3] must be equally likely to be returned.
// Example: return [3, 1, 2]
solution.reset();      // Resets the array back to its original configuration [1,2,3]. Return [1, 2, 3]
solution.shuffle();    // Returns the random shuffling of array [1,2,3]. Example: return [1, 3, 2]
```
##### Constraints:
* 1 <= nums.length <= 50
* -10^6 <= nums[i] <= 10^6
* All the elements of nums are unique.
* At most 10^4 calls in total will be made to reset and shuffle.

### Solution:
```java
class Solution {
    int [] original, copy;
    public Solution(int[] nums) {
        original = nums;
        copy = new int[nums.length];
        copy = nums.clone();
    }
    
    public int[] reset() {
        //copy = original.clone();
        return original;
    }
    
    public int[] shuffle() {
        Random rand = new Random();
        for(int i = 0; i < copy.length/2; i++){
            int k = rand.nextInt(copy.length);
            int l = rand.nextInt(copy.length);
            swap(copy, k, l);
        }
        return copy;
    }

    public void swap(int[] nums, int i, int j){
        int t = nums[i];
        nums[i] = nums[j];
        nums[j] = t;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int[] param_1 = obj.reset();
 * int[] param_2 = obj.shuffle();
 */
```