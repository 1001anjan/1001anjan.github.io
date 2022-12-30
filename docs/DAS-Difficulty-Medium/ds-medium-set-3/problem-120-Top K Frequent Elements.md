---
layout: default
title: Top K Frequent Elements
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 20
permalink: /problem-120-Top K Frequent Elements/
---
# Top K Frequent Elements
Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

##### Example 1:
```markdown
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```
##### Example 2:
```markdown
Input: nums = [1], k = 1
Output: [1]
```
##### Constraints:
* 1 <= nums.length <= 10^5
* -10^4 <= nums[i] <= 10^4
* k is in the range [1, the number of unique elements in the array].
* It is guaranteed that the answer is unique.

* Follow up: Your algorithm's time complexity must be better than O(n log n), where n is the array's size.

### Solution:
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        List<Integer[]> list = new ArrayList<>();
        Arrays.sort(nums);
        int count = 1;
        for(int i = 0; i < nums.length - 1; i++){
            if(nums[i] == nums[i + 1]) count++;
            else{
                list.add(new Integer[]{nums[i], count});
                count = 1;
            }
        }
        list.add(new Integer[]{nums[nums.length - 1], count});

        Collections.sort(list, (a, b) -> {
            return b[1] - a[1];
        });

        int[] ans = new int[k];
        for(int i = 0; i < k; i++){
            ans[i] = list.get(i)[0];
        }

        return ans;
    }
}
```