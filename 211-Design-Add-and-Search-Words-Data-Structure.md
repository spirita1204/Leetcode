# 211. Design Add and Search Words Data Structure

Methods: DFS
Difficulty: Medium

Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the `WordDictionary` class:

- `WordDictionary()` Initializes the object.
- `void addWord(word)` Adds `word` to the data structure, it can be matched later.
- `bool search(word)` Returns `true` if there is any string in the data structure that matches `word` or `false` otherwise. `word` may contain dots `'.'` where dots can be matched with any letter.

**Example:**

```
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

**Constraints:**

- `1 <= word.length <= 25`
- `word` in `addWord` consists of lowercase English letters.
- `word` in `search` consist of `'.'` or lowercase English letters.
- There will be at most `3` dots in `word` for `search` queries.
- At most `104` calls will be made to `addWord` and `search`.

```jsx
class WordDictionary {
    TrieNode node;

    public WordDictionary() {
        node = new TrieNode();
    }
    
    public void addWord(String word) {
        TrieNode insertTridNode = node;//root指標不動

        for(int i = 0; i < word.length(); i++){
            char c = word.charAt(i);//當前字母
            if(insertTridNode.children[c - 'a'] == null){
                insertTridNode.children[c- 'a'] = new TrieNode();//給定當前結點val
            }
            insertTridNode = insertTridNode.children[c - 'a'];//到子node
        }
        insertTridNode.isLast = true;//字尾結點給true
    }
    
    public boolean search(String word) {
        return match(word.toCharArray(), 0, node);
    }
    
    private boolean match(char[] chs, int k, TrieNode node) {//backtracking
        if (k == chs.length) return node.isLast;// 到leaf
        if(chs[k] != '.'){
            boolean isMatch = (node.children[chs[k] - 'a'] != null) ? true : false;
            if(isMatch == false) return false;
            return match(chs, k + 1, node.children[chs[k] - 'a']);
        }else {
            for (int i = 0; i < node.children.length; i++) {//當為'.' 則 遍歷所有字母 a~z
                if (node.children[i] != null) {
                    if (match(chs, k + 1, node.children[i])) {
                        return true;
                    }
                }
            }
        }
        return false;
    }
}
class TrieNode {
    public boolean isLast; 
    public TrieNode[] children = new TrieNode[26];
}

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * boolean param_2 = obj.search(word);
 */
```