---
layout: default
title: Different Ways to Add Parentheses
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 12
permalink: /problem-112-Different Ways to Add Parentheses/
---
# Different Ways to Add Parentheses
Given a string expression of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. You may return the answer in any order.

The test cases are generated such that the output values fit in a 32-bit integer and the number of different results does not exceed 104.

##### Example 1:
```markdown
Input: expression = "2-1-1"
Output: [0,2]
Explanation:
((2-1)-1) = 0
(2-(1-1)) = 2
```
##### Example 2:
```markdown
Input: expression = "2*3-4*5"
Output: [-34,-14,-10,-10,10]
Explanation:
(2*(3-(4*5))) = -34
((2*3)-(4*5)) = -14
((2*(3-4))*5) = -10
(2*((3-4)*5)) = -10
(((2*3)-4)*5) = 10
```
##### Constraints:
* 1 <= expression.length <= 20
* expression consists of digits and the operator '+', '-', and '*'.
* All the integer values in the input expression are in the range [0, 99].

### Solution:
```java
class Solution {
    public List<Integer> diffWaysToCompute(String expression) {
        List<Integer> ans = new LinkedList<>();
        for(int i = 0; i < expression.length(); i++){
            char ch = expression.charAt(i);
            if(isOperator(ch)){
                List<Integer> part1 = diffWaysToCompute(expression.substring(0,i));
                List<Integer> part2 = diffWaysToCompute(expression.substring(i + 1));

                for(Integer p1 : part1){
                    for(Integer p2 : part2){
                        switch(ch){
                            case '+' : ans.add(p1 + p2); break;
                            case '-' : ans.add(p1 - p2); break;
                            case '*' : ans.add(p1 * p2); break;
                        }
                    }
                }
            }
        }
        if(ans.size() == 0) ans.add(Integer.valueOf(expression));
        return ans;
    }

    public boolean isOperator(char ch){
        if(ch == '+' || ch == '-' || ch == '*') return true;
        return false;
    }
}
```