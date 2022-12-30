---
layout: default
title: LRU Cache
parent: Medium Set 2
grand_parent: DSA Medium Difficulty
nav_order: 29
permalink: /problem-79-LRU Cache/
---
# LRU Cache
Design a data structure that follows the constraints of a Least Recently Used (LRU) cache.

Implement the LRUCache class:

* LRUCache(int capacity) Initialize the LRU cache with positive size capacity.
* int get(int key) Return the value of the key if the key exists, otherwise return -1.
* void put(int key, int value) Update the value of the key if the key exists. Otherwise, add the key-value pair to the cache. If the number of keys exceeds the capacity from this operation, evict the least recently used key.
The functions get and put must each run in O(1) average time complexity.

##### Example 1:
```markdown
Input
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
Output
[null, null, null, 1, null, -1, null, -1, 3, 4]

Explanation
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4
```
##### Constraints:
* 1 <= capacity <= 3000
* 0 <= key <= 10^4
* 0 <= value <= 10^5
* At most 2 * 105 calls will be made to get and put.

### Solution:
##### Time Limits exceeds 
```java
class LRUCache {
    Map<Integer, Integer> map;
    LinkedList<Integer> list ;
    int capacity;

    public LRUCache(int capacity) {
        map = new HashMap<>();
        list = new LinkedList<>();
        this.capacity = capacity;
    }
    
    public int get(int key) {
        Integer k = map.get(key);
        if(k == null) return -1;
        list.remove(new Integer(key));
        list.addFirst(key);
        return k;
    }
    
    public void put(int key, int value) {
        if(get(key) == -1){
            if(map.size() == capacity){
                map.remove(list.removeLast());
            }  
        } 
        else{
            list.remove(new Integer(key));
        } 
        list.addFirst(key);
        map.put(key, value);
    }
        
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```
##### using doubly linkedList
```java
import java.util.HashMap;
import java.util.Map;

class LRUCache {
    private static class Node{
        int key;
        int value;
        Node next;
        Node prev;

        Node(){}
        Node(int k, int v, Node n, Node p){
            key = k;
            value = v;
            next = n;
            prev = p;
        }
    }

    private Map<Integer, Node> map;
    private Node head;
    private Node tail;
    private int capacity;

    public LRUCache(int capacity) {
        map = new HashMap<>();
        head = tail = null;
        this.capacity = capacity;
    }

    public int get(int key) {
        Node node = map.get(key);
        if(node == null) return -1;
        moveNodeToBegining(node);
        return node.value;
    }

    public void put(int key, int value) {
        Node node = map.get(key);
        if(node != null){
            node.value = value;
            moveNodeToBegining(node);
        }else{
            node = new Node(key, value, null, null);
            addNode(node);
            if(capacity < map.size()) removeNode();
        }
    }

    private void addNode(Node node){
        if(head == null && tail == null){
            head = tail = node;
            map.put(node.key, node);
            return;
        }
        node.next = head;
        head.prev = node;
        node.prev = null;
        head = node;
        map.put(node.key, node);
    }

    private void removeNode(){
        if(head == tail && head != null){
            head = tail = null;
            return;
        }
        Node node = tail;
        tail = tail.prev;
        tail.next = null;
        map.remove(node.key);
    }

    private void moveNodeToBegining(Node node){
        if(node == head) return;
        if(tail == node) tail = tail.prev;
        node.prev.next = node.next;
        if(node.next != null )node.next.prev = node.prev;
        node.next = head;
        head.prev = node;
        node.prev = null;
        head = node;
    }
}
```