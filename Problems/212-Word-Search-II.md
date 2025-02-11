# 212. Word Search II

Methods: DFS
Data structure: Trie
Difficulty: Hard

Hard

Topics

Companies

Hint

Given an `m x n` `board` of characters and a list of strings `words`, return *all words on the board*.

Each word must be constructed from letters of sequentially adjacent cells, where **adjacent cells** are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/11/07/search1.jpg](https://assets.leetcode.com/uploads/2020/11/07/search1.jpg)

```
Input: board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]
Output: ["eat","oath"]

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/11/07/search2.jpg](https://assets.leetcode.com/uploads/2020/11/07/search2.jpg)

```
Input: board = [["a","b"],["c","d"]], words = ["abcb"]
Output: []

```

**Constraints:**

- `m == board.length`
- `n == board[i].length`
- `1 <= m, n <= 12`
- `board[i][j]` is a lowercase English letter.
- `1 <= words.length <= 3 * 104`
- `1 <= words[i].length <= 10`
- `words[i]` consists of lowercase English letters.
- All the strings of `words` are unique

```java
class Solution {
    public List<String> findWords(char[][] board, String[] words) {
        List<String> res = new ArrayList<>();
        TrieNode root = buildTrie(words);// 將words 建成Trie;

        for (int x = 0; x < board.length; x++) {
            for (int y = 0; y < board[0].length; y++) {
                dfs(board, root, x, y, res);
            }
        }
        return res;
    }

    public void dfs(char[][] board, TrieNode root, int x, int y, List<String> res) {
        // out of bound
        if (x < 0 || y < 0 || x >= board.length || y >= board[0].length || board[x][y] == '0') {
            return;
        }
        char ch = board[x][y];
        if (ch == '#')// 走過
            return;
        if (root.children[ch - 'a'] == null)// leaf
            return;

        root = root.children[ch - 'a'];

        if (root.word != null) { // found one leaf
            res.add(root.word);
            root.word = null; // de-duplicate
        }
        // 當前走過避免重複
        board[x][y] = '#';
        /* recursion on all 4 sides for next letter, if works: return true */
        dfs(board, root, x + 1, y, res);// 右
        dfs(board, root, x - 1, y, res);// 左
        dfs(board, root, x, y + 1, res);// 下
        dfs(board, root, x, y - 1, res);// 上
        // 當下一輪要變回來
        board[x][y] = ch;
    }

    private TrieNode buildTrie(String[] words) {
        TrieNode root = new TrieNode();
        for (String w : words) {
            TrieNode p = root;
            for (char c : w.toCharArray()) {
                int i = c - 'a';
                if (p.children[i] == null)
                    p.children[i] = new TrieNode();
                p = p.children[i];
            }
            p.word = w;// leaf
        }
        return root;
    }
}

class TrieNode {
    public String word;
    public TrieNode[] children = new TrieNode[26];
}

```