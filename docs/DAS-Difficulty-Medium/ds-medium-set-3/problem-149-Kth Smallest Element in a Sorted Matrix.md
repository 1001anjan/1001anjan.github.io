---
layout: default
title: Kth Smallest Element in a Sorted Matrix
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 49
permalink: /problem-149-Kth Smallest Element in a Sorted Matrix/
---
# Kth Smallest Element in a Sorted Matrix
Given an n x n matrix where each of the rows and columns is sorted in ascending order, return the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

You must find a solution with a memory complexity better than O(n2).

##### Example 1:
```markdown
Input: matrix = [[1,5,9],[10,11,13],[12,13,15]], k = 8
Output: 13
Explanation: The elements in the matrix are [1,5,9,10,11,12,13,13,15], and the 8th smallest number is 13
```
##### Example 2:
```markdown
Input: matrix = [[1,5,9],[10,11,13],[12,13,15]], k = 8
Output: 13
Explanation: The elements in the matrix are [1,5,9,10,11,12,13,13,15], and the 8th smallest number is 13
```
##### Constraints:
* n == matrix.length == matrix[i].length
* 1 <= n <= 300
* -10^9 <= matrix[i][j] <= 10^9
* All the rows and columns of matrix are guaranteed to be sorted in non-decreasing order.
* 1 <= k <= n^2

### Solution:
###### Complexity:
* Time: O(M * N * logK), where M <= 300 is the number of rows, N <= 300 is the number of columns.
* Space: O(K), space for heap which stores up to k elements.
```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> Integer.compare(b, a));
        for(int i = 0; i < matrix.length; i++){
            for(int j = 0; j < matrix[0].length; j++){
                pq.offer(matrix[i][j]);
                while(pq.size() > k) pq.poll();
            }
        }

        return pq.poll();
    }
}
```

##### Solution 2: Min Heap to find kth smallest element from amongst N sorted list
* Since each of the rows in matrix are already sorted, we can understand the problem as finding the kth smallest element from amongst M sorted rows.
* We start the pointers to point to the beginning of each rows, then we iterate k times, for each time ith, the top of the minHeap is the ith smallest element in the matrix. We pop the top from the minHeap then add the next element which has the same row with that top to the minHeap.

![](../../assets/images/ds/47843946-761b-49f9-a06f-5a973fca3ddc_1625719598.4144652.png)
##### Complexity:
* Time: O(K * logK)
* Space: O(K)

```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> Integer.compare(a[0], b[0]));

        for(int i = 0; i < Math.min(matrix.length, k); i++) pq.offer(new int[]{matrix[i][0], i, 0});
        for(int i = 1; i < k; i++){
            int[] top = pq.poll();
            if(top[2] + 1 < matrix[0].length) pq.offer(new int[]{matrix[top[1]][top[2] + 1], top[1], top[2] + 1});
        }
        return pq.poll()[0];
    }
}
```

### ✔️ Solution 3: Binary Search
##### Algorithm

* Start with left = minOfMatrix = matrix[0][0] and right = maxOfMatrix = matrix[n-1][n-1].
* Find the mid of the left and the right. This middle number is NOT necessarily an element in the matrix.
* If countLessOrEqual(mid) >= k, we keep current ans = mid and try to find smaller value by searching in the left side. Otherwise, we search in the right side.
* Since ans is the smallest value which countLessOrEqual(ans) >= k, so it's the k th smallest element in the matrix.

##### How to count number of elements less or equal to x efficiently?
* Since our matrix is sorted in ascending order by rows and columns.
* We use two pointers, one points to the rightmost column c = n-1, and one points to the lowest row r = 0.
* If matrix[r][c] <= x then the number of elements in row r less or equal to x is (c+1) (Because row[r] is sorted in ascending order, so if matrix[r][c] <= x then matrix[r][c-1] is also <= x). Then we go to next row to continue counting.
* Else if matrix[r][c] > x, we decrease column c until matrix[r][c] <= x (Because column is sorted in ascending order, so if matrix[r][c] > x then matrix[r+1][c] is also > x).

##### Time complexity for counting: O(M+N).
![](../../assets/images/ds/fc7abf43-7537-41ee-addc-7b73b219c9eb_1625657181.1571143.png)
```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        
        int left = matrix[0][0];
        int right = matrix[matrix.length - 1][matrix[0].length - 1];
        int ans = -1;
        while(left <= right){
            int mid = (left + right) >> 1;
            if(countLessOrEquals(matrix, mid) >= k){
                ans = mid;
                right = mid - 1;
            }else{
                left = mid + 1;
            }
        }
        return ans;
    }

    public int countLessOrEquals(int[][] mat, int x){
        int count = 0;
        int c = mat[0].length - 1;
        for(int r = 0; r < mat.length; r++){
            while(c >= 0 && x < mat[r][c]) c --;
            count += c + 1;
        }
        return count;
    }
}
```





