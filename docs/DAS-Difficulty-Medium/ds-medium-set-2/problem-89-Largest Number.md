---
layout: default
title: Largest Number
parent: Medium Set 2
grand_parent: DSA Medium Difficulty
nav_order: 39
permalink: /problem-89-Largest Number/
---
# Largest Number
Given a list of non-negative integers nums, arrange them such that they form the largest number and return it.

Since the result may be very large, so you need to return a string instead of an integer.

##### Example 1:
```markdown
Input: nums = [10,2]
Output: "210"
```
##### Example 2:
```markdown
Input: nums = [3,30,34,5,9]
Output: "9534330"
```
##### Constraints:
* 1 <= nums.length <= 100
* 0 <= nums[i] <= 10^9

### Solution:
```java
class Solution {
    public String largestNumber(int[] nums) {
        List<Integer> list = new ArrayList<>();
        for(int n : nums) list.add(n);

        Collections.sort(list, (a, b) -> {
            String a1 = String.valueOf(a) + String.valueOf(b);
            String b1 = String.valueOf(b) + String.valueOf(a);
            return b1.compareTo(a1);
        });
        // after sorting if first element is 0
        if(list.get(0) == 0) return "0";
        StringBuilder sb = new StringBuilder();
        for(int n : list) sb.append(n);
        return sb.toString();
    }
}
```