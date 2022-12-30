---
layout: default
title: Random Pick Index
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 47
permalink: /problem-147-Random Pick Index/
---
# Random Pick Index
Given an integer array nums with possible duplicates, randomly output the index of a given target number. You can assume that the given target number must exist in the array.

Implement the Solution class:

* Solution(int[] nums) Initializes the object with the array nums.
* int pick(int target) Picks a random index i from nums where nums[i] == target. If there are multiple valid i's, then each index should have an equal probability of returning.

##### Example 1:
```markdown
Input
["Solution", "pick", "pick", "pick"]
[[[1, 2, 3, 3, 3]], [3], [1], [3]]
Output
[null, 4, 0, 2]

Explanation
Solution solution = new Solution([1, 2, 3, 3, 3]);
solution.pick(3); // It should return either index 2, 3, or 4 randomly. Each index should have equal probability of returning.
solution.pick(1); // It should return 0. Since in the array only nums[0] is equal to 1.
solution.pick(3); // It should return either index 2, 3, or 4 randomly. Each index should have equal probability of returning.
```
##### Constraints:
* 1 <= nums.length <= 2 * 10^4
* -2^31 <= nums[i] <= 2^31 - 1
* target is an integer from nums.
* At most 10^4 calls will be made to pick.

### Solution:
```java
class Solution {

    private HashMap<Integer, List<Integer>> indices;
    private Random rand;
    
    public Solution(int[] nums) {
        this.rand = new Random();
        this.indices = new HashMap<Integer, List<Integer>>();
        int l = nums.length;
        for (int i = 0; i < l; ++i) {
            if (!this.indices.containsKey(nums[i])) {
                this.indices.put(nums[i], new ArrayList<>());
            }
            this.indices.get(nums[i]).add(i);
        }
    }
    
    public int pick(int target) {
        int l = indices.get(target).size();
        // pick an index at random
        int randomIndex = indices.get(target).get(rand.nextInt(l));
        return randomIndex;
    }
}
```