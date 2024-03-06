---
layout: default
title: X of a Kind in a Deck of Cards
parent: Easy Set 14
grand_parent: DSA Easy
nav_order: 2
permalink: /problem-402-X of a Kind in a Deck of Cards/
---
# X of a Kind in a Deck of Cards
You are given an integer array deck where deck[i] represents the number written on the ith card.

Partition the cards into one or more groups such that:

* Each group has exactly x cards where x > 1, and
* All the cards in one group have the same integer written on them.
Return true if such partition is possible, or false otherwise.

##### Example 1:
```markdown
Input: deck = [1,2,3,4,4,3,2,1]
Output: true
Explanation: Possible partition [1,1],[2,2],[3,3],[4,4].
```
##### Example 2:
```markdown
Input: deck = [1,1,1,2,2,2,3,3]
Output: false
Explanation: No possible partition.
```
##### Constraints:
* 1 <= deck.length <= 10^4
* 0 <= deck[i] < 10^4

### Solution:
```java
class Solution {
    public boolean hasGroupsSizeX(int[] deck) {
        if(deck.length == 1) return false;
        int[] dp = new int[10000];
        for(int n : deck) dp[n]++;
        int minCount = Integer.MAX_VALUE;
        for(int n : dp) {
            if(n != 0) minCount = Math.min(minCount,n);
        }
        int i = 2;
        for(; i <= minCount; i++){
            boolean f = true;
               for(int n : dp){
                if(n != 0 && (n%i != 0)){
                    f = false; 
                    break;
                } 
            }
            if(f) break;
        }
        return i <= minCount;
    }
}
```
##### Improvement
```java
class Solution {
    public boolean hasGroupsSizeX(int[] deck) {
        int[] count = new int[10000];
        for (int c: deck)
            count[c]++;

        int g = -1;
        for (int i = 0; i < 10000; ++i)
            if (count[i] > 0) {
                if (g == -1)
                    g = count[i];
                else
                    g = gcd(g, count[i]);
            }

        return g >= 2;
    }

    public int gcd(int x, int y) {
        return x == 0 ? y : gcd(y%x, x);
    }
}
```
##### Complexity Analysis
* Time Complexity: O(Nlog^2 N)where N is the number of votes. If there are Ci cards with number i, then each gcd operation is naively O(log^2Ci). Better bounds exist, but are outside the scope of this article to develop.
* Space Complexity: O(N).
