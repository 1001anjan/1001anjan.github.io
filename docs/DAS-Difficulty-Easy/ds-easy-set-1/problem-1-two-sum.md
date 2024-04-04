---
layout: default
title: Two Sum
parent: Easy Set 1
grand_parent: DSA Easy
nav_order: 1
permalink: /problem-1-two-sum/

---

# 1. Two Sum
{: .no_toc }


Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.



### Example 1:
```markdown
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

### Example 2:
```markdown
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

### Example 3:
```markdown
Input: nums = [3,3], target = 6
Output: [0,1]
```

### Constraints:
```markdown
2 <= nums.length <= 104
-109 <= nums[i] <= 109
-109 <= target <= 109
```
Only one valid answer exists.

### Solution
Time Complexity: O(n) Space Complexity: O(n)
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap();
        int [] result = new int[2];
        result[0] = -1;
        result[1] = -1;
        for(int i=0; i<nums.length; i++){
            if(map.containsKey(target - nums[i])){
                result[0] = map.get(target - nums[i]);
                result[1] = i;
            }else{
                map.put(nums[i],i);
            }
        }
        return result;
    }
}
```

### Related solution
Since elements are not sorted, we can sort the list in O(nlog(n)) complexity. Space complexity O(1)
```java
class Solution {
    public boolean twoSum(int[] nums, int target) {
        Arrays.sort(nums);
        int i = 0;
        int j = nums.length - 1;
        while(i<j){
            if(nums[i] + nums[j] == target){
                return true;
            }
            if(nums[i] + nums[j] > target){
                j--;
            }else{
                i++;
            }
        }
        return false;
    }
}
```