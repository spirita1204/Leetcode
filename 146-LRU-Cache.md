# 146. LRU Cache

Data structure: Hash Table, Set
Difficulty: Medium

Medium

Topics

Companies

Design a data structure that follows the constraints of a [**Least Recently Used (LRU) cache**](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU).

Implement the `LRUCache` class:

- `LRUCache(int capacity)` Initialize the LRU cache with **positive** size `capacity`.
- `int get(int key)` Return the value of the `key` if the key exists, otherwise return `1`.
- `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, **evict** the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.

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
- `0 <= key <= 104`
- `0 <= value <= 105`
- At most `2 * 105` calls will be made to `get` and `put`.

```java
class LRUCache {
    int capacity;
    Map<Integer, Node> hm = new HashMap<>();
    // 不使用TreeSet 自訂義Node需要給定comparable 才會作動 此處單純需記錄插入順序
    Set<Node> s = new LinkedHashSet<>();

    public LRUCache(int capacity) {
        this.capacity = capacity;
    }

    public int get(int key) {
        if(!hm.containsKey(key)) return -1;// 未存在
        Node node = hm.get(key);
        s.remove(node);
        s.add(node);// 重新排序順序
        
        return node.value;
    }

    public void put(int key, int value) {
        if(hm.containsKey(key)){//[1, 1], [1, 2]
            hm.get(key).value = value;
            get(key);// 重複->重新排列在s中位置
            return;
        }
        if(s.size() == capacity) {// 容量超過
            // 刪除s中最初 
            Node node = s.iterator().next();
            s.remove(node);
            // 再透過s結果 刪除hm中key
            hm.remove(node.key);
        }
        // 將Node塞入
        Node node = new Node(key, value);
        hm.put(key, node);
        s.add(node);
    }
}

class Node {
    int key;
    int value;

    public Node(int key, int value) {
        this.key = key;
        this.value = value;
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```