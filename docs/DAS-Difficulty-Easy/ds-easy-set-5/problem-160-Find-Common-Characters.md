---
layout: default
title: Find Common Characters
parent: Easy Set 5
grand_parent: DSA Easy
nav_order: 30
permalink: /problem-160-Find-Common-Characters/
---
# Find Common Characters

Given a string array words, return an array of all characters that show up in all strings within the words (including duplicates). You may return the answer in any order.

##### Example 1:
```markdown
Input: words = ["bella","label","roller"]
Output: ["e","l","l"]
```
##### Example 2:
```markdown
Input: words = ["cool","lock","cook"]
Output: ["c","o"]
```
##### Constraints:
* 1 <= words.length <= 100
* 1 <= words[i].length <= 100
* words[i] consists of lowercase English letters.

### Solution:
```java
class Solution {
    public List<String> commonChars(String[] words) {
        List<String> ans = new ArrayList<>();
        Map<Character, Integer> m1 = new HashMap<>();
        // constracting first word
        for(char c : words[0].toCharArray())
            m1.put(c,m1.getOrDefault(c,0)+1);
        
        for(int i = 1; i < words.length; i++){
            Map<Character, Integer> m2 = new HashMap<>();
            for(char c : words[i].toCharArray())
                m2.put(c,m2.getOrDefault(c,0)+1);
            // find common char and store min value or remove uncommon
            Map<Character, Integer> m3 = new HashMap<>();
            for(char c : m2.keySet()){
                if(m1.containsKey(c))
                    m3.put(c,Math.min(m1.get(c),m2.get(c)));
            }
            m1 = m3;
        }
        // constract ans
        for(char c : m1.keySet()){
            for(int i = 1; i<= m1.get(c); i++)
                ans.add(String.valueOf(c));
        }
        
        return ans;
    }
}
```
```java
class Solution {
    public List<String> commonChars(String[] words) {
        List<String> res = new ArrayList<>();
        
        for(char ch = 'a'; ch <= 'z'; ch++) {
            int minCountOfCh = Integer.MAX_VALUE;
            for(String word : words) {
                int currChCount = 0;
                for(char currCh : word.toCharArray()) {
                    if(currCh == ch) {
                        currChCount++;
                    }
                }   
                minCountOfCh = Math.min(minCountOfCh, currChCount);
            }
            
            for(int i = 0; i < minCountOfCh; i++) {
                res.add(String.valueOf(ch));
            }
        }
        return res;
    }
}
```
```java
class Solution {
       public List<String> commonChars(String[] words) {
        List<String> ans = new ArrayList<>();
        int[] freq = new int[26];
        Arrays.fill(freq, Integer.MAX_VALUE);

        for (String s : words) {
            int[] temp = new int[26];
            for (int i = 0; i < s.length(); i++) {
                int index = (int) s.charAt(i) - 'a';
                temp[index]++;
            }

            for (int i = 0; i < 26; i++) {
                freq[i] = Math.min(temp[i], freq[i]);
            }
        }

        for (int i = 0; i < 26; i++) {
            while (freq[i]-- > 0) {
                System.out.print(i + " ");
                char c = (char) (i + 97);
                ans.add("" + c);
            }
        }
        return ans;
    }
}
```