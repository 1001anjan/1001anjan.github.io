---
layout: default
title: Minimum Rounds to Complete All Tasks
parent: Medium Set 4
grand_parent: DSA Medium
nav_order: 7
permalink: /problem-157-Minimum Rounds to Complete All Tasks/
---
# Minimum Rounds to Complete All Tasks
You are given a 0-indexed integer array tasks, where tasks[i] represents the difficulty level of a task. In each round, you can complete either 2 or 3 tasks of the same difficulty level.

Return the minimum rounds required to complete all the tasks, or -1 if it is not possible to complete all the tasks.

##### Example 1:
```markdown
Input: tasks = [2,2,3,3,2,4,4,4,4,4]
Output: 4
Explanation: To complete all the tasks, a possible plan is:
- In the first round, you complete 3 tasks of difficulty level 2.
- In the second round, you complete 2 tasks of difficulty level 3.
- In the third round, you complete 3 tasks of difficulty level 4.
- In the fourth round, you complete 2 tasks of difficulty level 4.  
  It can be shown that all the tasks cannot be completed in fewer than 4 rounds, so the answer is 4.
```
##### Example 2:
```markdown
Input: tasks = [2,3,3]
Output: -1
Explanation: There is only 1 task of difficulty level 2, but in each round, you can only complete either 2 or 3 tasks of the same difficulty level. Hence, you cannot complete all the tasks, and the answer is -1.
```
##### Constraints:
* 1 <= tasks.length <= 10^5
* 1 <= tasks[i] <= 10^9

### Solution:
```java
class Solution {
    public int minimumRounds(int[] tasks) {
       Map<Integer, Integer> mp = new HashMap<>();
       for(int n : tasks) mp.put(n, mp.getOrDefault(n, 0) + 1);
       int count = 0;
       for(int n : mp.values()){
           int c = process(n);
           if(c == -1) return -1;
           count += c;
       } 
       return count;
    }

    public int process(int n){
        if(n % 3 == 0) return n / 3;
        int c3 = n / 3, c2 = 1;
        while(c2 * 2 <= n){
            int value = c3 * 3 + c2 * 2;
            if(value == n) return c3 > 0 ? c3 + c2 : c2;
            if(value > n){
                c3 --;
                c2 ++;
            }
        }

        return -1;
    }
}
```
```java
class Solution {
    public int minimumRounds(int[] tasks) {
        Map<Integer, Integer> freq = new HashMap();
        // Store the frequencies in the map.
        for (int task : tasks) {
            freq.put(task, freq.getOrDefault(task, 0) + 1);
        }

        int minimumRounds = 0;
        // Iterate over the task's frequencies.
        for (int count : freq.values()) {
            // If the frequency is 1, it's not possible to complete tasks.
            if (count == 1) {
                return - 1;
            }

            if (count % 3 == 0) {
                // Group all the task in triplets.
                minimumRounds += count / 3;
            } else {
                // If count % 3 = 1; (count / 3 - 1) groups of triplets and 2 pairs.
                // If count % 3 = 2; (count / 3) groups of triplets and 1 pair.
                minimumRounds += count / 3 + 1;
            }
        }

        return minimumRounds;
    }
}
```