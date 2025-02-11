# 2416. Sum of Prefix Scores of Strings

Data structure: Trie
Difficulty: Hard

You are given an array `words` of size `n` consisting of **non-empty** strings.

We define the **score** of a string `word` as the **number** of strings `words[i]` such that `word` is a **prefix** of `words[i]`.

- For example, if `words = ["a", "ab", "abc", "cab"]`, then the score of `"ab"` is `2`, since `"ab"` is a prefix of both `"ab"` and `"abc"`.

Return *an array* `answer` *of size* `n` *where* `answer[i]` *is the **sum** of scores of every **non-empty** prefix of* `words[i]`.

**Note** that a string is considered as a prefix of itself.

**Example 1:**

```
Input: words = ["abc","ab","bc","b"]
Output: [5,4,3,2]
Explanation: The answer for each string is the following:
- "abc" has 3 prefixes: "a", "ab", and "abc".
- There are 2 strings with the prefix "a", 2 strings with the prefix "ab", and 1 string with the prefix "abc".
The total is answer[0] = 2 + 2 + 1 = 5.
- "ab" has 2 prefixes: "a" and "ab".
- There are 2 strings with the prefix "a", and 2 strings with the prefix "ab".
The total is answer[1] = 2 + 2 = 4.
- "bc" has 2 prefixes: "b" and "bc".
- There are 2 strings with the prefix "b", and 1 string with the prefix "bc".
The total is answer[2] = 2 + 1 = 3.
- "b" has 1 prefix: "b".
- There are 2 strings with the prefix "b".
The total is answer[3] = 2.

```

**Example 2:**

```
Input: words = ["abcd"]
Output: [4]
Explanation:
"abcd" has 4 prefixes: "a", "ab", "abc", and "abcd".
Each prefix has a score of one, so the total is answer[0] = 1 + 1 + 1 + 1 = 4.

```

**Constraints:**

- `1 <= words.length <= 1000`
- `1 <= words[i].length <= 1000`
- `words[i]` consists of lowercase English letters.

Hint 1

What data structure will allow you to efficiently keep track of the score of each prefix?

---

Hint 2

Use a Trie. Insert all the words into it, and keep a counter at each node that will tell you how many times we have visited each prefix.

---

```java
class Solution {
    public int[] sumPrefixScores(String[] words) {
        int len = words.length;
        int[] res = new int[len];
        TrieNode root = new TrieNode();

        // 先做出trie(每個節點給定權重)
        for(String word : words) {
            TrieNode insertTridNode = root;// root指標不動
            for(int i = 0; i < word.length(); i++){
                char c = word.charAt(i);//當前字母
                if(insertTridNode.children[c - 'a'] == null){
                    insertTridNode.children[c- 'a'] = new TrieNode(1);//給定當前結點val
                } else {// 已有經過過
                    insertTridNode.children[c - 'a'].val++;
                }
                insertTridNode = insertTridNode.children[c - 'a'];//到子node
            }
            insertTridNode.last = true;
        }
        // 搜尋
        int idx = 0;
        for(String word : words) {
            int sum = 0;
            TrieNode searchTrieNode = root;
            for(int i = 0; i < word.length(); i++){
                char c = word.charAt(i);
                sum += searchTrieNode.children[c - 'a'].val;
                searchTrieNode = searchTrieNode.children[c - 'a'];//到子node
            }
            res[idx++] = sum;
        }
        return res;
    }
}

class TrieNode {
    public int val;
    public TrieNode[] children = new TrieNode[26];
    public boolean last;
    public TrieNode() {};
    public TrieNode(int val) {
        this.val = val;
    }
}
```