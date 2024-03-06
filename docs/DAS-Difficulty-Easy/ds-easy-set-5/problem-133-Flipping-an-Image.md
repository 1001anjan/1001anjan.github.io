---
layout: default
title: Flipping an Image
parent: Easy Set 5
grand_parent: DSA Easy
nav_order: 3
permalink: /problem-133-Flipping-an-Image/
---
# Flipping an Image

Given an n x n binary matrix image, flip the image horizontally, then invert it, and return the resulting image.

To flip an image horizontally means that each row of the image is reversed.

For example, flipping [1,1,0] horizontally results in [0,1,1].
To invert an image means that each 0 is replaced by 1, and each 1 is replaced by 0.

For example, inverting [0,1,1] results in [1,0,0].

##### Example 1:
```markdown
Input: image = [[1,1,0],[1,0,1],[0,0,0]]
Output: [[1,0,0],[0,1,0],[1,1,1]]
Explanation: First reverse each row: [[0,1,1],[1,0,1],[0,0,0]].
Then, invert the image: [[1,0,0],[0,1,0],[1,1,1]]
```
##### Example 2:
```markdown
Input: image = [[1,1,0,0],[1,0,0,1],[0,1,1,1],[1,0,1,0]]
Output: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
Explanation: First reverse each row: [[0,0,1,1],[1,0,0,1],[1,1,1,0],[0,1,0,1]].
Then invert the image: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
```
##### Constraints:
* n == image.length
* n == image[i].length
* 1 <= n <= 20
* images[i][j] is either 0 or 1.

### Solution:
```java
class Solution {
    public int[][] flipAndInvertImage(int[][] image) {
        int m = image.length;
        int n = image[0].length;
        // flip image
        for(int i=0; i<m; i++){
            int s = 0;
            int e = n - 1;
            while(s<e){
                int t = image[i][s];
                image[i][s] = image[i][e];
                image[i][e] = t;
                s++;
                e--;
            }
        }
        // Invert image
        for(int i=0; i<m; i++)
            for(int j=0; j<n; j++)
                if(image[i][j] == 1) image[i][j] = 0;
                else image[i][j] = 1;
        
        return image; 
    }
}
```
```java
class Solution {
    public int[][] flipAndInvertImage(int[][] A) {
        int C = A[0].length;
        for (int[] row: A)
            for (int i = 0; i < (C + 1) / 2; ++i) {
                int tmp = row[i] ^ 1;
                row[i] = row[C - 1 - i] ^ 1;
                row[C - 1 - i] = tmp;
            }

        return A;
    }
}
```