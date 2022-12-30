---
layout: default
title: Positions of Large Groups
parent: Easy Set 5
grand_parent: DSA Easy Difficulty
nav_order: 2
permalink: /problem-132-Positions-of-Large-Groups/
---
# Positions of Large Groups

In a string s of lowercase letters, these letters form consecutive groups of the same character.

For example, a string like s = "abbxxxxzyy" has the groups "a", "bb", "xxxx", "z", and "yy".

A group is identified by an interval [start, end], where start and end denote the start and end indices (inclusive) of the group. In the above example, "xxxx" has the interval [3,6].

A group is considered large if it has 3 or more characters.

Return the intervals of every large group sorted in increasing order by start index.

##### Example 1:
```markdown
Input: s = "abbxxxxzzy"
Output: [[3,6]]
Explanation: "xxxx" is the only large group with start index 3 and end index 6.
```
##### Example 2:
```markdown
Input: s = "abc"
Output: []
Explanation: We have groups "a", "b", and "c", none of which are large groups.
```
##### Example 3:
```markdown
Input: s = "abcdddeeeeaabbbcd"
Output: [[3,5],[6,9],[12,14]]
Explanation: The large groups are "ddd", "eeee", and "bbb".
```
##### Constraints:
* 1 <= s.length <= 1000
* s contains lowercase English letters only.

### Solution:
```java
class Solution {
    public List<List<Integer>> largeGroupPositions(String s) {
        List<List<Integer>> ans = new ArrayList();
        int l = 0;
        int u = 0;
        for(int i=1; i<s.length(); i++){
           if(s.charAt(i-1) == s.charAt(i)){
               u++;
           }else{
                if(u - l +1 >= 3){
                    ans.add(Arrays.asList(new Integer[]{l, u}));
                } 
              l = u = i;
           } 
        }
        if(u - l +1 >= 3){
            ans.add(Arrays.asList(new Integer[]{l, u}));
        } 
        return ans;
    }
}
```