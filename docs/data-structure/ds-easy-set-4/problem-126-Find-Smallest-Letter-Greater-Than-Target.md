---
layout: default
title: Find Smallest Letter Greater Than Target
parent: Data Structure Easy Set 4
grand_parent: Data Structure
nav_order: 26
permalink: /problem-126-Find-Smallest-Letter-Greater-Than-Target/
---
# Find Smallest Letter Greater Than Target

Given a characters array letters that is sorted in non-decreasing order and a character target, return the smallest character in the array that is larger than target.

Note that the letters wrap around.

For example, if target == 'z' and letters == ['a', 'b'], the answer is 'a'.

##### Example 1:
```markdown
Input: letters = ["c","f","j"], target = "a"
Output: "c"
```
##### Example 2:
```markdown
Input: letters = ["c","f","j"], target = "c"
Output: "f"
```
##### Example 3:
```markdown
Input: letters = ["c","f","j"], target = "d"
Output: "f"
```
##### Constraints:
* 2 <= letters.length <= 104
* letters[i] is a lowercase English letter.
* letters is sorted in non-decreasing order.
* letters contains at least two different characters.
* target is a lowercase English letter.

### Solution:
```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        for(int i = 0; i<letters.length; i++){
            if(letters[i]>target) return letters[i];
        }
        return letters[0];
    }
}
```
#### Binary search
```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        int lo = 0, hi = letters.length;
        while (lo < hi) {
            int mi = lo + (hi - lo) / 2;
            if (letters[mi] <= target) lo = mi + 1;
            else hi = mi;
        }
        return letters[lo % letters.length];
    }
}
```