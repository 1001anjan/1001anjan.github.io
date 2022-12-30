---
layout: default
title: Kth Distinct String in an Array
parent: Easy Set 11
grand_parent: DSA Easy Difficulty
nav_order: 7
permalink: /problem-317-Kth Distinct String in an Array/
---
# Kth Distinct String in an Array

A distinct string is a string that is present only once in an array.

Given an array of strings arr, and an integer k, return the kth distinct string present in arr. If there are fewer than k distinct strings, return an empty string "".

Note that the strings are considered in the order in which they appear in the array.

##### Example 1:
```markdown
Input: arr = ["d","b","c","b","c","a"], k = 2
Output: "a"
Explanation:
The only distinct strings in arr are "d" and "a".
"d" appears 1st, so it is the 1st distinct string.
"a" appears 2nd, so it is the 2nd distinct string.
Since k == 2, "a" is returned.
```
##### Example 2:
```markdown
Input: arr = ["aaa","aa","a"], k = 1
Output: "aaa"
Explanation:
All strings in arr are distinct, so the 1st string "aaa" is returned.
```
##### Example 3:
```markdown
Input: arr = ["a","b","a"], k = 3
Output: ""
Explanation:
The only distinct string is "b". Since there are fewer than 3 distinct strings, we return an empty string "".
```
##### Constraints:
* 1 <= k <= arr.length <= 1000
* 1 <= arr[i].length <= 5
* arr[i] consists of lowercase English letters.

### Solution:
```java
class Solution {
    public String kthDistinct(String[] arr, int k) {
        Set<String> set = new LinkedHashSet<>();
        Set<String> dupSet = new HashSet<>();
        for(String s : arr){
            if(set.contains(s)){
                dupSet.add(s);
            }else{
                set.add(s);
            }
        }
        for(String s : dupSet){
          set.remove(s);  
        }
        if(k > set.size()) return "";
        int i = 1;
        for(String str : set){
            if(i == k) return str;
            i++;
        }
        return "";
    }
}
```