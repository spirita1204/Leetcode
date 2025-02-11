# 677. Map Sum Pairs

Data structure: Trie
Difficulty: Medium

Medium

Topics

Companies

Design a map that allows you to do the following:

- Maps a string key to a given value.
- Returns the sum of the values that have a key with a prefix equal to a given string.

Implement the `MapSum` class:

- `MapSum()` Initializes the `MapSum` object.
- `void insert(String key, int val)` Inserts the `key-val` pair into the map. If the `key` already existed, the original `key-value` pair will be overridden to the new one.
- `int sum(string prefix)` Returns the sum of all the pairs' value whose `key` starts with the `prefix`.

**Example 1:**

```
Input
["MapSum", "insert", "sum", "insert", "sum"]
[[], ["apple", 3], ["ap"], ["app", 2], ["ap"]]
Output
[null, null, 3, null, 5]

Explanation
MapSum mapSum = new MapSum();
mapSum.insert("apple", 3);
mapSum.sum("ap");           // return 3 (apple = 3)
mapSum.insert("app", 2);
mapSum.sum("ap");           // return 5 (apple +app = 3 + 2 = 5)

```

**Constraints:**

- `1 <= key.length, prefix.length <= 50`
- `key` and `prefix` consist of only lowercase English letters.
- `1 <= val <= 1000`
- At most `50` calls will be made to `insert` and `sum`.

```java
class MapSum {
    private TrieNode root;
    private Map<String, Integer> hm = new HashMap<>();

    public MapSum() {
        root = new TrieNode();
    }
	
    public void insert(String key, int val) {
        int oriVal = 0;// 判斷是否重複
        if(hm.containsKey(key)){
            oriVal = hm.get(key);
        }
        hm.put(key, val);
        TrieNode insertTridNode = root;// root指標不動
        if(oriVal != 0) {
            val -= oriVal;// 要扣掉
        }
        for (int i = 0; i < key.length(); i++) {
            char c = key.charAt(i);// 當前字母
            if (insertTridNode.children[c - 'a'] == null) {
                insertTridNode.children[c - 'a'] = new TrieNode(val);// 給定當前結點val
            }else {
                insertTridNode.children[c - 'a'].val += val;
            }
            insertTridNode = insertTridNode.children[c - 'a'];// 到子node
        }
    }

    public int sum(String prefix) {
        TrieNode sumTrieNode = root;

        for(int i = 0; i < prefix.length(); i++){
            char c = prefix.charAt(i);
            if(sumTrieNode.children[c - 'a'] == null){
                return 0;
            }
            sumTrieNode = sumTrieNode.children[c - 'a'];//到子node
        }
        return sumTrieNode.val;
    }
}

class TrieNode {
    public int val;
    public TrieNode[] children = new TrieNode[26];

    public TrieNode() {};
    public TrieNode(int val) {
        this.val = val;
    }
}

/**
 * Your MapSum object will be instantiated and called as such:
 * MapSum obj = new MapSum();
 * obj.insert(key,val);
 * int param_2 = obj.sum(prefix);
 */
```