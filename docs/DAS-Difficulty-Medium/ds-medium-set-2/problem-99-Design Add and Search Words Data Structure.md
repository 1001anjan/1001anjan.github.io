---
layout: default
title: Design Add and Search Words Data Structure
parent: Medium Set 2
grand_parent: DSA Medium
nav_order: 49
permalink: /problem-99-Design Add and Search Words Data Structure/
---
# Design Add and Search Words Data Structure
Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the WordDictionary class:

* WordDictionary() Initializes the object.
* void addWord(word) Adds word to the data structure, it can be matched later.
* bool search(word) Returns true if there is any string in the data structure that matches word or false otherwise. word may contain dots '.' where dots can be matched with any letter.

##### Example:
```markdown
Input
["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
Output
[null,null,null,null,false,true,true,true]

Explanation
WordDictionary wordDictionary = new WordDictionary();
wordDictionary.addWord("bad");
wordDictionary.addWord("dad");
wordDictionary.addWord("mad");
wordDictionary.search("pad"); // return False
wordDictionary.search("bad"); // return True
wordDictionary.search(".ad"); // return True
wordDictionary.search("b.."); // return True
```
##### Constraints:
* 1 <= word.length <= 25
* word in addWord consists of lowercase English letters.
* word in search consist of '.' or lowercase English letters.
* There will be at most 3 dots in word for search queries.
* At most 10^4 calls will be made to addWord and search.

### Solution
```java
class WordDictionary {
    private static class TreeNode{
        boolean exists;
        TreeNode[] children = new TreeNode[26];
    }

    private TreeNode root;
   
    public WordDictionary() {
        root = new TreeNode();    
    }
    
    public void addWord(String word) {
        TreeNode node = root;
        for(int i = 0; i < word.length(); i++){
            int id = word.charAt(i) - 'a';
            if(node.children[id] == null) node.children[id] = new TreeNode();
            node = node.children[id];
        }
        node.exists = true;
    }
    
    public boolean search(String word) {
        return search(word, 0, root);
    }

    private boolean search(String word, int start, TreeNode node){
        if(start >= word.length()) return node.exists;
        char ch = word.charAt(start);
        if(start == word.length() - 1){
            
            if(ch == '.'){
                for(int i = 0; i < 26; i++){
                    if(node.children[i] != null && node.children[i].exists) return true;
                }
                return false;
            }else{
                int id = ch - 'a';
                TreeNode n = node.children[id];
                if(n == null) return false;
                return n.exists;
            }
        }

        if(ch == '.'){
            for(int i = 0; i < 26; i++){
                if(node.children[i] != null && search(word, start + 1, node.children[i])) return true;
            }
        }else{
            int i = ch - 'a';
            if(node.children[i] != null && search(word, start + 1, node.children[i])) return true;
        }

        return false;
    }
}

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * boolean param_2 = obj.search(word);
 */
```