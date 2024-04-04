---
layout: default
title: Maximum Ice Cream Bars
parent: Medium Set 4
grand_parent: DSA Medium
nav_order: 9
permalink: /problem-159-Maximum Ice Cream Bars/
---
# Maximum Ice Cream Bars
It is a sweltering summer day, and a boy wants to buy some ice cream bars.

At the store, there are n ice cream bars. You are given an array costs of length n, where costs[i] is the price of the ith ice cream bar in coins. The boy initially has coins coins to spend, and he wants to buy as many ice cream bars as possible.

Return the maximum number of ice cream bars the boy can buy with coins coins.

Note: The boy can buy the ice cream bars in any order.

##### Example 1:
```markdown
Input: costs = [1,3,2,4,1], coins = 7
Output: 4
Explanation: The boy can buy ice cream bars at indices 0,1,2,4 for a total price of 1 + 3 + 2 + 1 = 7.
```
##### Example 2:
```markdown
Input: costs = [10,6,8,7,7,8], coins = 5
Output: 0
Explanation: The boy cannot afford any of the ice cream bars.
```
##### Example 3:
````markdown
Input: costs = [1,6,3,1,2,5], coins = 20
Output: 6
Explanation: The boy can buy all the ice cream bars for a total price of 1 + 6 + 3 + 1 + 2 + 5 = 18.
````
##### Constraints:
* costs.length == n
* 1 <= n <= 10^5
* 1 <= costs[i] <= 10^5
* 1 <= coins <= 10^8

### Solution:
```java
class Solution {
    public int maxIceCream(int[] costs, int coins) {
        Arrays.sort(costs);
        int count = 0;

        for(int n : costs){
            if(coins >= n){
                coins -= n;
                count++;
            }else break;
        }

        return count;
    }
}
```
##### Using counting sort
```java
class Solution {
    public int maxIceCream(int[] costs, int coins) {
        int m = costs[0];
        for (int cost : costs) m = Math.max(m, cost);

        int[] freq_arr = new int[m + 1];

        for(int c : costs) freq_arr[c] ++;

        int count = 0;

        for(int i = 1; i < freq_arr.length; i++){
            if(freq_arr[i] == 0) continue;
            if(freq_arr[i] > coins) break;

            // Count how many icecreams of 'cost' we can pick with our 'coins'.
            // Either we can pick all ice creams of 'cost' or we will be limited by remaining 'coins'.
            int max = Math.min(freq_arr[i], coins/i);
            count += max;
            coins -= i * max;
            System.out.println(max+" "+coins+" "+count);
        }

        return count;
    }
}
```