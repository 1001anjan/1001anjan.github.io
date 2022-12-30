---
layout: default
title: Merge Intervals
parent: Medium Set 1
grand_parent: DSA Medium Difficulty
nav_order: 31
permalink: /problem-31-Merge Intervals/
---
# Merge Intervals
Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

##### Example 1:
```markdown
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
```
##### Example 2:
```markdown
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```
##### Constraints:
* 1 <= intervals.length <= 10^4
* intervals[i].length == 2
* 0 <= starti <= endi <= 10^4

### Solution:
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        List<List<Integer>> list = new LinkedList<>();
        Arrays.sort(intervals, (a,b) ->{
            if(a[0] != b[0]) return a[0] - b[0];
            return a[1] - b[1];
        });
        int i1 = intervals[0][0];
        int i2 = intervals[0][1];

        int i = 1;

        while(i < intervals.length){
            if(i2 >= intervals[i][0]){
                i2 = Math.max(i2, intervals[i][1]);
            }else{
                List<Integer> l = new LinkedList<>();
                l.add(i1);
                l.add(i2);
                list.add(l);
                i1 = intervals[i][0];
                i2 = intervals[i][1];
            }
            i++;
        }
        List<Integer> l = new LinkedList<>();
        l.add(i1);
        l.add(i2);
        list.add(l);

        int[][] ans = new int[list.size()][2];
        i = 0;
        for(List<Integer> l1 : list){
            ans[i][0] = l1.get(0);
            ans[i][1] = l1.get(1);
            i++;
        }

        return ans;

    }
}
```
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        LinkedList<int[]> merged = new LinkedList<>();
        for (int[] interval : intervals) {
            // if the list of merged intervals is empty or if the current
            // interval does not overlap with the previous, simply append it.
            if (merged.isEmpty() || merged.getLast()[1] < interval[0]) {
                merged.add(interval);
            }
            // otherwise, there is overlap, so we merge the current and previous
            // intervals.
            else {
                merged.getLast()[1] = Math.max(merged.getLast()[1], interval[1]);
            }
        }
        return merged.toArray(new int[merged.size()][]);
    }
}
```
