---
layout: default
title: Network Delay Time
parent: Medium Set 4
grand_parent: DSA Medium
nav_order: 20
permalink: /problem-170-Network Delay Time/
---
# Network Delay Time
You are given a network of n nodes, labeled from 1 to n. You are also given times, a list of travel times as directed edges times[i] = (ui, vi, wi), where ui is the source node, vi is the target node, and wi is the time it takes for a signal to travel from source to target.

We will send a signal from a given node k. Return the minimum time it takes for all the n nodes to receive the signal. If it is impossible for all the n nodes to receive the signal, return -1.

##### Example 1:

```markdown
Input: times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2
Output: 2
```
##### Example 2:
````markdown
Input: times = [[1,2,1]], n = 2, k = 1
Output: 1
````
##### Example 3:
```markdown
Input: times = [[1,2,1]], n = 2, k = 2
Output: -1
```
##### Constraints:
* 1 <= k <= n <= 100
* 1 <= times.length <= 6000
* times[i].length == 3
* 1 <= ui, vi <= n
* ui != vi
* 0 <= wi <= 100
* All the pairs (ui, vi) are unique. (i.e., no multiple edges.)

### Solution:
```java
class Solution {
    public int networkDelayTime(int[][] times, int n, int k) {
        Map<Integer, List<Integer>> adj = new HashMap<>();
        Map<String, Integer> weight = new HashMap<>();
        int[] dp = new int[n + 1];
        Arrays.fill(dp, 1000);
        
        for(int[] arr : times){
            adj.computeIfAbsent(arr[0], value -> new ArrayList<>()).add(arr[1]);
            weight.put(arr[0]+"*"+arr[1], arr[2]);
        }
        Queue<Integer> q = new LinkedList<>();
        q.offer(k);
        dp[k] = 0;
        while(!q.isEmpty()){
            int node = q.poll();
            if(!adj.containsKey(node)) continue;
            for(int child : adj.get(node)){
                String path = node+"*"+child;
                int arrTime = dp[node] + weight.get(path);
                if(dp[child] > arrTime){
                    dp[child] = arrTime;
                    q.offer(child);
                } 
            }
        }
        int max = -1;
        for(int i = 1; i < dp.length; i++){
            max = Math.max(max, dp[i]);
        }
        return max == 1000? -1: max;
    }
}
```
##### Same BFS approach but improved in the String operation
```java
class Solution {
    // Adjacency list
    Map<Integer, List<Pair<Integer, Integer>>> adj = new HashMap<>();

    private void BFS(int[] signalReceivedAt, int sourceNode) {
        Queue<Integer> q = new LinkedList<>();
        q.add(sourceNode);
        
        // Time for starting node is 0
        signalReceivedAt[sourceNode] = 0;
        
        while (!q.isEmpty()) {
            int currNode = q.remove();
            
            if (!adj.containsKey(currNode)) {
                continue;
            }
            
            // Broadcast the signal to adjacent nodes
            for (Pair<Integer, Integer> edge : adj.get(currNode)) {
                int time = edge.getKey();
                int neighborNode = edge.getValue();
                
                // Fastest signal time for neighborNode so far
                // signalReceivedAt[currNode] + time : 
                // time when signal reaches neighborNode
                int arrivalTime = signalReceivedAt[currNode] + time;
                if (signalReceivedAt[neighborNode] > arrivalTime) {
                    signalReceivedAt[neighborNode] = arrivalTime;
                    q.add(neighborNode);
                }
            }
        }
    }
    
    public int networkDelayTime(int[][] times, int n, int k) {
        // Build the adjacency list
        for (int[] time : times) {
            int source = time[0];
            int dest = time[1];
            int travelTime = time[2];
            
            adj.putIfAbsent(source, new ArrayList<>());
            adj.get(source).add(new Pair(travelTime, dest));
        }
        
        int[] signalReceivedAt = new int[n + 1];
        Arrays.fill(signalReceivedAt, Integer.MAX_VALUE);
        
        BFS(signalReceivedAt, k);
        
        int answer = Integer.MIN_VALUE;
        for (int i = 1; i <= n; i++) {
            answer = Math.max(answer, signalReceivedAt[i]);
        }
        
        // INT_MAX signifies atleat one node is unreachable
        return answer == Integer.MAX_VALUE ? -1 : answer;
    }
}
```