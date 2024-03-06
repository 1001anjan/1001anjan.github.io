---
layout: default
title:  Guess Number Higher or Lower
parent: Easy Set 3
grand_parent: DSA Easy
nav_order: 5
permalink: /problem-68-Guess-Number-Higher-or-Lower/
---
# Guess Number Higher or Lower

We are playing the Guess Game. The game is as follows:

I pick a number from 1 to n. You have to guess which number I picked.

Every time you guess wrong, I will tell you whether the number I picked is higher or lower than your guess.

You call a pre-defined API int guess(int num), which returns three possible results:

* -1: Your guess is higher than the number I picked (i.e. num > pick).
* 1: Your guess is lower than the number I picked (i.e. num < pick).
* 0: your guess is equal to the number I picked (i.e. num == pick).
* Return the number that I picked.

##### Example 1:
```markdown
Input: n = 10, pick = 6
Output: 6
```
##### Example 2:
```markdown
Input: n = 1, pick = 1
Output: 1
```
##### Example 3:
```markdown
Input: n = 2, pick = 1
Output: 1
```
##### Constraints:
* 1 <= n <= 231 - 1
* 1 <= pick <= n

### Solution
#### Binary search
```java
/** 
 * Forward declaration of guess API.
 * @param  num   your guess
 * @return 	     -1 if num is higher than the picked number
 *			      1 if num is lower than the picked number
 *               otherwise return 0
 * int guess(int num);
 */

public class Solution extends GuessGame {
    public int guessNumber(int n) {
        int s = 1;
        int e = n;
        int r;
        int mid = -1;
        while(true){
            mid = (s+e)/2;
           r = guess(mid);
            if(r == 0) break;;
            if(r == 1){
                s = mid+1;
            }else{
                e = mid-1;
            }
        }
        return mid;
    }
}
```
#### Ternary Search
```java

```