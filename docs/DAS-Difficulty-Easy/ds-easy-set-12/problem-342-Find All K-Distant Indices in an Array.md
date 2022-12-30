---
layout: default
title: Find All K-Distant Indices in an Array
parent: Easy Set 12
grand_parent: DSA Easy Difficulty
nav_order: 2
permalink: /problem-342-Find All K-Distant Indices in an Array/
---
# Find All K-Distant Indices in an Array
You are given a 0-indexed integer array nums and two integers key and k. A k-distant index is an index i of nums for which there exists at least one index j such that |i - j| <= k and nums[j] == key.

Return a list of all k-distant indices sorted in increasing order.

##### Example 1:
```markdown
Input: nums = [3,4,9,1,3,9,5], key = 9, k = 1
Output: [1,2,3,4,5,6]
Explanation: Here, nums[2] == key and nums[5] == key.
- For index 0, |0 - 2| > k and |0 - 5| > k, so there is no j where |0 - j| <= k and nums[j] == key. Thus, 0 is not a k-distant index.
- For index 1, |1 - 2| <= k and nums[2] == key, so 1 is a k-distant index.
- For index 2, |2 - 2| <= k and nums[2] == key, so 2 is a k-distant index.
- For index 3, |3 - 2| <= k and nums[2] == key, so 3 is a k-distant index.
- For index 4, |4 - 5| <= k and nums[5] == key, so 4 is a k-distant index.
- For index 5, |5 - 5| <= k and nums[5] == key, so 5 is a k-distant index.
- For index 6, |6 - 5| <= k and nums[5] == key, so 6 is a k-distant index.
  Thus, we return [1,2,3,4,5,6] which is sorted in increasing order.
```
##### Example 2:
```markdown
Input: nums = [2,2,2,2,2], key = 2, k = 2
Output: [0,1,2,3,4]
Explanation: For all indices i in nums, there exists some index j such that |i - j| <= k and nums[j] == key, so every index is a k-distant index.
Hence, we return [0,1,2,3,4].
```
##### Constraints:
* 1 <= nums.length <= 1000
* 1 <= nums[i] <= 1000
* key is an integer from the array nums.
* 1 <= k <= nums.length

### Solution:
```java
class Solution {
    public List<Integer> findKDistantIndices(int[] nums, int key, int k) {
        Set<Integer> s = new HashSet<>();
        for(int i = 0; i < nums.length; i++){
            if(nums[i] == key){
                if(s.add(i)){
                    for(int j = i - 1; j >= 0 && j >= i - k ; j--){
                        if(!s.add(j)) break;
                    }
                }
                for(int j = i + 1; j < nums.length && j <= i + k ; j++){
                    s.add(j);
                }
            }
        }
        
        List<Integer> ans = s.stream().collect(Collectors.toList());
        Collections.sort(ans);
        return ans;
    }
}
```
##### Improvement and O(n) complexity
```java
class Solution {
    public List<Integer> findKDistantIndices(int[] nums, int key, int k) {
        List<Integer> ans = new ArrayList<>();
        for(int i = 0, j =0, lastVisited = 0; i < nums.length; i++){
            if(nums[i] == key){
                for(j = Math.max(lastVisited,i - k); j < Math.min(nums.length,i + k + 1); j++){
                    ans.add(j);
                }
                lastVisited = j;
            }
        }
        return ans;
    }
}
```