---
layout: default
title: Longest Consecutive Sequence
parent: Medium Set 4
grand_parent: DSA Medium Difficulty
nav_order: 4
permalink: /problem-154-Longest Consecutive Sequence/
---
# Longest Consecutive Sequence
Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in O(n) time.

##### Example 1:
```markdown
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```
##### Example 2:
```markdown
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
```
##### Constraints:
* 0 <= nums.length <= 10^5
* -10^9 <= nums[i] <= 10^9

### Solution:
```java
class Solution {
    public int longestConsecutive(int[] nums) {
        if(nums.length == 0) return 0;
        Arrays.sort(nums);
        int s = 0, e = 0, i = 1;
        int max = 1;
        while(i < nums.length){
            if(nums[i - 1] + 1 == nums[i]){
                e++;
            }else if(nums[i - 1] == nums[i]){   // for duplicate numbers, not counting 
                e++;
                s++;
            }else{
                s = i;
                e = i;
            }
            i++;
            max = Math.max(max, e - s + 1);
        }
        return max;
    }
}
```
#### NOTE: n*log(n) is better
##### Another way but slow 
```java
class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> num_set = new HashSet<Integer>();
        for (int num : nums) {
            num_set.add(num);
        }

        int longestStreak = 0;

        for (int num : num_set) {
            if (!num_set.contains(num-1)) {
                int currentNum = num;
                int currentStreak = 1;

                while (num_set.contains(currentNum+1)) {
                    currentNum += 1;
                    currentStreak += 1;
                }

                longestStreak = Math.max(longestStreak, currentStreak);
            }
        }

        return longestStreak;
    }
}
```