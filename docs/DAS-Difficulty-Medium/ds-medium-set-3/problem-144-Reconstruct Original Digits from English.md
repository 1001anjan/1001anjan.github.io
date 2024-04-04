---
layout: default
title: Reconstruct Original Digits from English
parent: Medium Set 3
grand_parent: DSA Medium
nav_order: 44
permalink: /problem-144-Reconstruct Original Digits from English/
---
# Reconstruct Original Digits from English
Given a string s containing an out-of-order English representation of digits 0-9, return the digits in ascending order.

##### Example 1:
```markdown
Input: s = "owoztneoer"
Output: "012"
```
##### Example 2:
```markdown
Input: s = "fviefuro"
Output: "45"
```
##### Constraints:
* 1 <= s.length <= 10^5
* s[i] is one of the characters ["e","g","f","i","h","o","n","s","r","u","t","w","v","x","z"].
* s is guaranteed to be valid.

### Solution:
```java
class Solution {
    public String originalDigits(String s) {
       // one, two, three, four, five, six seven, eight, nine, zero

       // 0 --> if z is available
       // 1 --> 
       // 4/5 --> f must present, 
        // 4 --> u 
        // x --> for six
       // 7 --> if s  
       // 8 --> g must be present
       // 9 --> for n -> 9/1

       List<Integer> list = new ArrayList<>();
       int[] dp = new int[26];
       for(char ch : s.toCharArray()) dp[ch - 'a']++;

       // adding all zeros
       while(dp[25] > 0){
           list.add(0);
           dp[25]--;
           dp['e' - 'a']--;
           dp['r' - 'a']--;
           dp['o' - 'a']--;
       }
       // adding six
        while(dp['x' - 'a'] > 0){
            list.add(6);
            dp['s' - 'a']--;
            dp['i' - 'a']--;
            dp['x' - 'a']--;
        }

       // adding all seven
       while(dp['s' - 'a'] > 0){
           list.add(7);
           dp['s' - 'a']--;
           dp['e' - 'a'] -= 2;
           dp['v' - 'a']--;
           dp['n' - 'a']--;
       }

        
       // adding all eight
       while(dp['g' - 'a'] > 0){
            list.add(8);
            dp['e' - 'a']--;
            dp['i' - 'a']--;
            dp['g' - 'a']--;
            dp['h' - 'a']--;
            dp['t' - 'a']--;
       }

       // adding all four 
       while(dp['u' - 'a'] > 0){
           list.add(4);
           dp['f' - 'a']--;
           dp['o' - 'a']--;
           dp['u' - 'a']--;
           dp['r' - 'a']--;
       }

       // since four's added now five can added by f only
       while(dp['f' - 'a'] > 0){
           list.add(5);
           dp['f' - 'a']--;
           dp['i' - 'a']--;
           dp['v' - 'a']--;
           dp['e' - 'a']--;
       }

       // since zero and four added so now we can add three
       while(dp['r' - 'a'] > 0){
           list.add(3);
           dp['t' - 'a']--;
           dp['h' - 'a']--;
           dp['r' - 'a']--;
           dp['e' - 'a'] -= 2;
       }

       // adding two by w
       while(dp['w' - 'a'] > 0){
           list.add(2);
           dp['t' - 'a']--;
           dp['w' - 'a']--;
           dp['o' - 'a']--;
       }

        // now adding nine by i
        while(dp['i' - 'a'] > 0){
            list.add(9);
            dp['n' - 'a']--;
            dp['i' - 'a']--;
            dp['n' - 'a']--;
            dp['e' - 'a']--;
        }

        // now adding one
        while(dp['n' - 'a'] > 0){
            list.add(1);
            dp['o' - 'a']--;
            dp['n' - 'a']--;
            dp['e' - 'a']--;
        }

        // sorting the list
        Collections.sort(list);
        StringBuilder sb = new StringBuilder();
        for(int n : list) sb.append(String.valueOf(n));

        return sb.toString();
    }
}
```

```java
class Solution {
    public String originalDigits(String s) {
       // one, two, three, four, five, six seven, eight, nine, zero

       List<Integer> list = new ArrayList<>();
       int[] dp = new int[128];
       for(char ch : s.toCharArray()) dp[ch]++;

       // adding all zeros
       while(dp['z'] > 0){
           list.add(0);
           dp['z']--;
           dp['e']--;
           dp['r']--;
           dp['o']--;
       }
       // adding six
        while(dp['x'] > 0){
            list.add(6);
            dp['s']--;
            dp['i']--;
            dp['x']--;
        }

       // adding all seven
       while(dp['s'] > 0){
           list.add(7);
           dp['s']--;
           dp['e'] -= 2;
           dp['v']--;
           dp['n']--;
       }

        
       // adding all eight
       while(dp['g'] > 0){
            list.add(8);
            dp['e']--;
            dp['i']--;
            dp['g']--;
            dp['h']--;
            dp['t']--;
       }

       // adding all four 
       while(dp['u'] > 0){
           list.add(4);
           dp['f']--;
           dp['o']--;
           dp['u']--;
           dp['r']--;
       }

       // since four's added now five can added by f only
       while(dp['f'] > 0){
           list.add(5);
           dp['f']--;
           dp['i']--;
           dp['v']--;
           dp['e']--;
       }

       // since zero and four added so now we can add three
       while(dp['r'] > 0){
           list.add(3);
           dp['t']--;
           dp['h']--;
           dp['r']--;
           dp['e'] -= 2;
       }

       // adding two by w
       while(dp['w'] > 0){
           list.add(2);
           dp['t']--;
           dp['w']--;
           dp['o']--;
       }

        // now adding nine by i
        while(dp['i'] > 0){
            list.add(9);
            dp['n']--;
            dp['i']--;
            dp['n']--;
            dp['e']--;
        }

        // now adding one
        while(dp['n'] > 0){
            list.add(1);
            dp['o']--;
            dp['n']--;
            dp['e']--;
        }

        // sorting the list
        Collections.sort(list);
        StringBuilder sb = new StringBuilder();
        for(int n : list) sb.append(String.valueOf(n));

        return sb.toString();
    }
}
```

##### Clean solution

* zero, two, six eight, have distinct character z, w, x, g
* other characters are only shared by word with known count and only another word with unknown count, like six and seven share 's', seven and five share 'v'

```java
class Solution {
    public String originalDigits(String s) {
        int[] cc = new int[256];
        int[] dc = new int[10];
        for (char c: s.toCharArray()) {
            ++cc[c];
        }
        String[] order = {"zero", "six", "seven", "five", "four", "two", "eight", "three", "one", "nine"};
        char[] flag = {'z', 'x', 's', 'v', 'f', 'w', 'g', 'r', 'o', 'i'};
        int[] digits = {0, 6, 7, 5, 4, 2, 8, 3, 1, 9};
        for (int i = 0; i< 10; ++i) {
            int n = cc[flag[i]];
            if (n > 0) {
                dc[digits[i]] = n;
                for (char c: order[i].toCharArray()) cc[c] -= n;
            }
        }
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i <= 9; ++i) {
            for (int j = 0; j < dc[i]; ++j)
                sb.append(i);
        }
        return sb.toString();
    }
}
```