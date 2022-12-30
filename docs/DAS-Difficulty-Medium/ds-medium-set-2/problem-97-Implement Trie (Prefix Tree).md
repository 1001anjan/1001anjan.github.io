---
layout: default
title: Implement Trie (Prefix Tree)
parent: Medium Set 2
grand_parent: DSA Medium Difficulty
nav_order: 47
permalink: /problem-97-Implement Trie (Prefix Tree)/
---
# Implement Trie (Prefix Tree)
A trie (pronounced as "try") or prefix tree is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

* Trie() Initializes the trie object.
* void insert(String word) Inserts the string word into the trie.
* boolean search(String word) Returns true if the string word is in the trie (i.e., was inserted before), and false otherwise.
* boolean startsWith(String prefix) Returns true if there is a previously inserted string word that has the prefix prefix, and false otherwise.

##### Example 1:
```markdown
Input
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
Output
[null, null, true, false, true, null, true]

Explanation
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // return True
trie.search("app");     // return False
trie.startsWith("app"); // return True
trie.insert("app");
trie.search("app");     // return True
```
##### Constraints:
* 1 <= word.length, prefix.length <= 2000
* word and prefix consist only of lowercase English letters.
* At most 3 * 10^4 calls in total will be made to insert, search, and startsWith.

### Solution:
```java
class Trie {

    private static class TreeNode{
        boolean exists;
        TreeNode[] children = new TreeNode[26];
    }

    private TreeNode root;

    public Trie() {
        root = new TreeNode();    
    }
    
    public void insert(String word) {
        TreeNode node = root;
        for(int i = 0; i < word.length(); i++){
            int id = word.charAt(i) - 'a';
            if(node.children[id] == null) node.children[id] = new TreeNode();
            node = node.children[id];
        }
        node.exists = true;
    }
    
    public boolean search(String word) {
        TreeNode node = root;
        for(int i = 0; i < word.length(); i++){
            int id =  word.charAt(i) - 'a';
            if(node.children[id] == null) return false;
            node = node.children[id];
        }
        return node.exists;
    }
    
    public boolean startsWith(String prefix) {
        TreeNode node = root;
        for(int i = 0; i < prefix.length(); i++){
            int id =  prefix.charAt(i) - 'a';
            if(node.children[id] == null) return false;
            node = node.children[id];
        }
        for(int i = 0; i < 26; i++){
            if(node.children[i] != null) return true;
        }
        return node.exists;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```