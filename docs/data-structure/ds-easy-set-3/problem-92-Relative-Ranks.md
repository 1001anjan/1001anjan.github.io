---
layout: default
title: Relative Ranks
parent: Data Structure Easy Set 3
grand_parent: Data Structure
nav_order: 29
permalink: /problem-92-Relative-Ranks/
---
# Relative Ranks

You are given an integer array score of size n, where score[i] is the score of the ith athlete in a competition. All the scores are guaranteed to be unique.

The athletes are placed based on their scores, where the 1st place athlete has the highest score, the 2nd place athlete has the 2nd highest score, and so on. The placement of each athlete determines their rank:

* The 1st place athlete's rank is "Gold Medal".
* The 2nd place athlete's rank is "Silver Medal".
* The 3rd place athlete's rank is "Bronze Medal".
* For the 4th place to the nth place athlete, their rank is their placement number (i.e., the xth place athlete's rank is "x").

Return an array answer of size n where answer[i] is the rank of the ith athlete.

##### Example 1:
````markdown
Input: score = [5,4,3,2,1]
Output: ["Gold Medal","Silver Medal","Bronze Medal","4","5"]
Explanation: The placements are [1st, 2nd, 3rd, 4th, 5th].
````
##### Example 2:
```markdown
Input: score = [10,3,8,9,4]
Output: ["Gold Medal","5","Bronze Medal","Silver Medal","4"]
Explanation: The placements are [1st, 5th, 3rd, 2nd, 4th].
```
##### Constraints:
* n == score.length
* 1 <= n <= 104
* 0 <= score[i] <= 106
* All the values in score are unique.

### Solution:
```java
class Solution {
    public String[] findRelativeRanks(int[] score) {
        String[] result = new String[score.length];
        List<Integer> temp = new ArrayList<>();
        for(int i: score) temp.add(i);
        Collections.sort(temp, Collections.reverseOrder()); 
        int index;
        for(int i = 0; i<score.length; i++){
            index = temp.indexOf(score[i]);
            if(index == 0){
                result[i] = "Gold Medal";
            }else if(index == 1){
                result[i] = "Silver Medal";
            }else if(index == 2){
                result[i] = "Bronze Medal";
            }else{
                result[i] = String.valueOf(index+1);
            }
        }
        return result;
    }
}
```
```java
class Solution {
    public String[] findRelativeRanks(int[] score) {
        int a[]=new int[score.length];
        for(int i=0;i<score.length;i++){
            a[i]=score[i];
        }
        Arrays.sort(score);
        String ans[]=new String[score.length];
        for(int i=score.length;i>0;i--){
            String rank=GetRank(score,i);
            int index=Search(a,score[i-1]);
            ans[index]=rank;
        }
        return ans;
    }
    static String GetRank(int score[],int pos){
        if(pos==score.length){
            return "Gold Medal";
        }
        else if(pos==score.length-1){
            return "Silver Medal";
        }
        else if(pos==score.length-2){
            return "Bronze Medal";
        }
        else
        {
            int a=score.length-pos+1;
            String s=Integer.toString(a);  
            return s;
        }
    }
    static int Search(int a[],int target){
        for(int i=0;i<a.length;i++){
            if(target==a[i]){
                return i;
            }
        }
        return -1;
    }
}
```
```java
class Solution {
    public String[] findRelativeRanks(int[] score) {
        final String GOLD = "Gold Medal";
        final String SILVER = "Silver Medal";
        final String BRONZE = "Bronze Medal";
        final String[] result = new String[score.length];
        PriorityQueue<Integer[]> pq = new PriorityQueue<>((arr1, arr2) -> arr2[0] - arr1[0]);
        for (int i = 0; i < score.length; i++) {
            pq.add(new Integer[]{score[i], i});
        }

        int k = 1;
        while (!pq.isEmpty()) {
            if (k <= 3) {
                if (k == 1)
                    result[pq.poll()[1]] = GOLD;
                if (k == 2)
                    result[pq.poll()[1]] = SILVER;
                if (k == 3)
                    result[pq.poll()[1]] = BRONZE;

            } else{
                result[pq.poll()[1]] = String.valueOf(k);
            }
                k++;
        }

        return result;
    }
}
```