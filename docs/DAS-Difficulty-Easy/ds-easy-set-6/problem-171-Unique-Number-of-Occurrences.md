---
layout: default
title: Unique Number of Occurrences
parent: Easy Set 6
grand_parent: DSA Easy Difficulty
nav_order: 11
permalink: /problem-171-Unique-Number-of-Occurrences/
---
# Unique Number of Occurrences

Given an array of integers arr, return true if the number of occurrences of each value in the array is unique, or false otherwise.

##### Example 1:
```markdown
Input: arr = [1,2,2,1,1,3]
Output: true
Explanation: The value 1 has 3 occurrences, 2 has 2 and 3 has 1. No two values have the same number of occurrences.
```
##### Example 2:
```markdown
Input: arr = [1,2]
Output: false
```
##### Example 3:
```markdown
Input: arr = [-3,0,1,-3,1,1,1,-3,10,0]
Output: true
```
##### Constraints:
* 1 <= arr.length <= 1000
* -1000 <= arr[i] <= 1000

### Solution:
```java
class Solution {
    public boolean uniqueOccurrences(int[] arr) {
        Map<Integer, Integer> m = new HashMap<>();
        for(int n : arr){
            m.put(n,m.getOrDefault(n,0) + 1);
        }
        int prev = Integer.MAX_VALUE;
        for(int n : m.values().stream().sorted().collect(Collectors.toList())){
            if(prev == n) return false;
            prev = n;
        }
        return true;
    }
}
```
#### Extra Memory but Time Complexity O(n)
```java
class Solution {
    public boolean uniqueOccurrences(int[] arr) {
        Map<Integer, Integer> m = new HashMap<>();
        for(int n : arr){
            m.put(n,m.getOrDefault(n,0) + 1);
        }
        Set<Integer> s = new HashSet();
        for(int n : m.values()) s.add(n);
        return s.size() == m.size();
    }
}
```

