# 208. Implement Trie (Prefix Tree)

Data structure: Trie
Difficulty: Medium

A [**trie**](https://en.wikipedia.org/wiki/Trie) (pronounced as "try") or **prefix tree** is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

- `Trie()` Initializes the trie object.
- `void insert(String word)` Inserts the string `word` into the trie.
- `boolean search(String word)` Returns `true` if the string `word` is in the trie (i.e., was inserted before), and `false` otherwise.
- `boolean startsWith(String prefix)` Returns `true` if there is a previously inserted string `word` that has the prefix `prefix`, and `false` otherwise.

**Example 1:**

```
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

**Constraints:**

- `1 <= word.length, prefix.length <= 2000`
- `word` and `prefix` consist only of lowercase English letters.
- At most `3 * 104` calls **in total** will be made to `insert`, `search`, and `startsWith`.

```java
class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }
    
    public void insert(String word) {
        TrieNode insertTridNode = root;//root指標不動

        for(int i = 0; i < word.length(); i++){
            char c = word.charAt(i);//當前字母
            if(insertTridNode.children[c - 'a'] == null){
                insertTridNode.children[c- 'a'] = new TrieNode();//給定當前結點val
            }
            insertTridNode = insertTridNode.children[c - 'a'];//到子node
        }
        insertTridNode.isLast = true;//字尾結點給true
    }
    
    public boolean search(String word) {//完整
        TrieNode searchTrieNode = root;

        for(int i = 0; i < word.length(); i++){
            char c = word.charAt(i);
            //System.out.println(c);
            //System.out.println(searchTrieNode.children[c - 'a'].val);
            if(searchTrieNode.children[c - 'a'] == null){
                return false;
            }
            searchTrieNode = searchTrieNode.children[c - 'a'];//到子node
        }
        return searchTrieNode.isLast;
    }
    
    public boolean startsWith(String prefix) {
        TrieNode startsWithTrieNode = root;

        for(int i = 0; i < prefix.length(); i++){
            char c = prefix.charAt(i);
            if(startsWithTrieNode.children[c - 'a'] == null) return false;
            startsWithTrieNode = startsWithTrieNode.children[c - 'a'];//到子node
        }
        return true;
    }
}

class TrieNode {

    public char val;

    public boolean isLast; 

    public TrieNode[] children = new TrieNode[26];
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```