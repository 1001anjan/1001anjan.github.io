---
layout: default
title: Maximum Repeating Substring
parent: Easy Set 9
grand_parent: DSA Easy Difficulty
nav_order: 1
permalink: /problem-251-Maximum-Repeating-Substring/
---
# Check If Two String Arrays are Equivalent

For a string sequence, a string word is k-repeating if word concatenated k times is a substring of sequence. The word's maximum k-repeating value is the highest value k where word is k-repeating in sequence. If word is not a substring of sequence, word's maximum k-repeating value is 0.

Given strings sequence and word, return the maximum k-repeating value of word in sequence.

##### Example 1:
```markdown
Input: sequence = "ababc", word = "ab"
Output: 2
Explanation: "abab" is a substring in "ababc".
```
##### Example 2:
```markdown
Input: sequence = "ababc", word = "ba"
Output: 1
Explanation: "ba" is a substring in "ababc". "baba" is not a substring in "ababc".
```
##### Example 3:
```markdown
Input: sequence = "ababc", word = "ac"
Output: 0
Explanation: "ac" is not a substring in "ababc".
```
##### Constraints:
* 1 <= sequence.length <= 100
* 1 <= word.length <= 100
* sequence and word contains only lowercase English letters.

### Solution:
```java
class Solution {
    public int maxRepeating(String sequence, String word) {
        StringBuilder umang = new StringBuilder(word);
        int count =0;
        while(true){
            if(sequence.contains(umang)){
                count+=1;
                umang.append(word);
            }
            else{
                return count;
            }
        }
    }
}
// The main concept here is , we have to  form a possible longest substring using concatenated 'word' in 'sequence' and keep increasing our count of repeating ' word'.
```