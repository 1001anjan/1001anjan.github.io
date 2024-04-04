---
layout: default
title: Find K Pairs with Smallest Sums
parent: Medium Set 4
grand_parent: DSA Medium
nav_order: 12
permalink: /problem-162-Find K Pairs with Smallest Sums/
---
# Find K Pairs with Smallest Sums
You are given two integer arrays nums1 and nums2 sorted in ascending order and an integer k.

Define a pair (u, v) which consists of one element from the first array and one element from the second array.

Return the k pairs (u1, v1), (u2, v2), ..., (uk, vk) with the smallest sums.

##### Example 1:
```markdown
Input: nums1 = [1,7,11], nums2 = [2,4,6], k = 3
Output: [[1,2],[1,4],[1,6]]
Explanation: The first 3 pairs are returned from the sequence: [1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]
```
##### Example 2:
```markdown
Input: nums1 = [1,1,2], nums2 = [1,2,3], k = 2
Output: [[1,1],[1,1]]
Explanation: The first 2 pairs are returned from the sequence: [1,1],[1,1],[1,2],[2,1],[1,2],[2,2],[1,3],[1,3],[2,3]
```
##### Example 3:
````markdown
Input: nums1 = [1,2], nums2 = [3], k = 3
Output: [[1,3],[2,3]]
Explanation: All possible pairs are returned from the sequence: [1,3],[2,3]
````
##### Constraints:
* 1 <= nums1.length, nums2.length <= 10^5
* -10^9 <= nums1[i], nums2[i] <= 10^9
* nums1 and nums2 both are sorted in ascending order.
* 1 <= k <= 10^4

### Solution:
```java
class Solution {
    public List<List<Integer>> kSmallestPairs(int[] nums1, int[] nums2, int k) {
        List<List<Integer>> ans = new ArrayList<>();
        // the check is not required as per Constraints for the problem
        if(nums1.length == 0 || nums2.length == 0 || k == 0) return ans;

        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> (a[0] + a[1] - b[0] - b[1]));

        for(int i = 0; i < Math.min(nums1.length , k); i++){
            // storing combination nums1[i], nums2[0], 0 -> first index of nums2
            pq.offer(new int[]{nums1[i], nums2[0], 0});
        }

        while(k-- > 0 && !pq.isEmpty()){
            int curr[] = pq.poll();
            ans.add(Arrays.asList(curr[0], curr[1]));
            if(curr[2] < nums2.length - 1) pq.offer(new int[]{curr[0], nums2[curr[2] + 1], curr[2] + 1});
        }

        return ans;
    }
}
```