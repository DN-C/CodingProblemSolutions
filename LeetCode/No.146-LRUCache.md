## Description

Design a data structure that follows the constraints of a **[Least Recently Used (LRU) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU)**.

Implement the `LRUCache` class:

- `LRUCache(int capacity)` Initialize the LRU cache with **positive** size `capacity`.
- `int get(int key)` Return the value of the `key` if the key exists, otherwise return `-1`.
- `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, **evict** the least recently used key.

**Follow up:**
Could you do `get` and `put` in `O(1)` time complexity?

 

**Example 1:**

```
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

 

**Constraints:**

- `1 <= capacity <= 3000`
- `0 <= key <= 3000`
- `0 <= value <= 104`
- At most `3 * 104` calls will be made to `get` and `put`.

## Thinking

HashMap + Double Link.

Or just LinkedHashMap.

## Solutions

~~~java
class LRUCache {
    class Node {
        int key, value;
        Node prev, next;
        
        Node(int k, int v) {
            key = k;
            value = v;
        }
        
        Node() {
            key = 0;
            value = 0;
        }
    }
    Map<Integer, Node> map;
    Node head, tail;
    int capacity, count;

    public LRUCache(int capacity) {
        map = new HashMap<Integer, Node>();
        head = new Node();
        tail = new Node();
        head.next = tail;
        tail.prev = head;
        this.capacity = capacity;
        this.count = 0;
    }
    
    public int get(int key) {
        if(map.containsKey(key)) {
            update(key);
            return map.get(key).value; 
        } else return -1;
        
    }
    
    public void put(int key, int value) {
        if(map.containsKey(key)) {
            map.get(key).value = value;
            update(key);
        } else {
            Node node = new Node(key, value);
            map.put(key, node);
            add(node);
            ++count;
        }
        check();
    }
    
    public void update(int key) {
        Node node = map.get(key);
        remove(node);
        add(node);
    }
    
    public void check() {
        while(count > capacity) {
            map.remove(tail.prev.key);
            remove(tail.prev);
            --count;
        }
    }
    
    public void remove(Node node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }
    
    public void add(Node node) {
        head.next.prev = node;
        node.next = head.next;
        head.next = node;
        node.prev = head;
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
~~~



## Further

[https://leetcode.com/problems/lru-cache/discuss/45939/Laziest-implementation%3A-Java's-LinkedHashMap-takes-care-of-everything](https://leetcode.com/problems/lru-cache/discuss/45939/Laziest-implementation%3A-Java's-LinkedHashMap-takes-care-of-everything)