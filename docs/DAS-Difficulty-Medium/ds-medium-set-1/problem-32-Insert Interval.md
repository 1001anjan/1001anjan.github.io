---
layout: default
title: Insert Interval
parent: Medium Set 1
grand_parent: DSA Medium
nav_order: 32
permalink: /problem-32-Insert Interval/
---
# Insert Interval
You are given an array of non-overlapping intervals intervals where intervals[i] = [starti, endi] represent the start and the end of the ith interval and intervals is sorted in ascending order by starti. You are also given an interval newInterval = [start, end] that represents the start and end of another interval.

Insert newInterval into intervals such that intervals is still sorted in ascending order by starti and intervals still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return intervals after the insertion.

##### Example 1:
```markdown
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
```
##### Example 2:
```markdown
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```
##### Constraints:
* 0 <= intervals.length <= 10^4
* intervals[i].length == 2
* 0 <= starti <= endi <= 10^5
* intervals is sorted by starti in ascending order.
* newInterval.length == 2
* 0 <= start <= end <= 10^5

### Solution: 
```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int[]> list = new LinkedList<>();
        
        // adding new item to sorted position 
        boolean added = false;
        for(int[] arr : intervals){
            if(!added){
                if(newInterval[0] == arr[0]){
                    if(newInterval[1] < arr[1]){
                        list.add(newInterval);
                        list.add(arr);
                    }else{
                        list.add(arr);
                        list.add(newInterval);
                    }
                    added = true;
                }else if(newInterval[0] < arr[0]){
                    list.add(newInterval);
                    list.add(arr);
                    added = true;
                }
            }
           list.add(arr); 
        }
        if(!added){
            list.add(newInterval);
        }
        // merging intervals
        LinkedList<int[]> merged = new LinkedList<>();
        for(int[] interval : list){
            if(merged.isEmpty() || merged.getLast()[1] < interval[0]){
                merged.add(interval);
            }else{
                merged.getLast()[1] = Math.max(merged.getLast()[1] , interval[1]);
            }
        }
        return merged.toArray(new int[merged.size()][]);
    }
}
```