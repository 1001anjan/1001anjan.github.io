---
layout: default
title: Generate Parentheses
parent: Medium Set 1
grand_parent: DSA Medium
nav_order: 13
permalink: /problem-13-Generate Parentheses/
---
# Generate Parentheses
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

##### Example 1:
```markdown
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```
##### Example 2:
```markdown
Input: n = 1
Output: ["()"]
```
##### Constraints:
* 1 <= n <= 8

### Solution:
```java
class Solution {
    public List<String> generateParenthesis(int n){
        if(n == 1){
            return new ArrayList(Arrays.asList("()"));
        }
        List<String> list = generateParenthesis(n - 1);
        Set<String> ans = new HashSet<>();
        for(String str : list){
            for(int i = 0; i < str.length(); i++){
                if(str.charAt(i) == '('){
                    ans.add(str.substring(0, i + 1)+"()"+str.substring(i + 1, str.length()));
                }
            }
            ans.add(str+"()");
        }
        return new ArrayList(ans);
    }
}
```
```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> ans = new ArrayList();
        if (n == 0) {
            ans.add("");
        } else {
            for (int c = 0; c < n; ++c)
                for (String left: generateParenthesis(c))
                    for (String right: generateParenthesis(n-1-c))
                        ans.add("(" + left + ")" + right);
        }
        return ans;
    }
}
```
```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> combinations = new ArrayList();
        generateAll(new char[2 * n], 0, combinations);
        return combinations;
    }

    public void generateAll(char[] current, int pos, List<String> result) {
        if (pos == current.length) {
            if (valid(current))
                result.add(new String(current));
        } else {
            current[pos] = '(';
            generateAll(current, pos+1, result);
            current[pos] = ')';
            generateAll(current, pos+1, result);
        }
    }

    public boolean valid(char[] current) {
        int balance = 0;
        for (char c: current) {
            if (c == '(') balance++;
            else balance--;
            if (balance < 0) return false;
        }
        return (balance == 0);
    }
}
```