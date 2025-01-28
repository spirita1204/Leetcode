# 648. Replace Words

Data structure: Trie
Difficulty: Medium

Medium

Topics

Companies

In English, we have a concept called **root**, which can be followed by some other word to form another longer word - let's call this word **derivative**. For example, when the **root** `"help"` is followed by the word `"ful"`, we can form a derivative `"helpful"`.

Given a `dictionary` consisting of many **roots** and a `sentence` consisting of words separated by spaces, replace all the derivatives in the sentence with the **root** forming it. If a derivative can be replaced by more than one **root**, replace it with the **root** that has **the shortest length**.

Return *the `sentence`* after the replacement.

**Example 1:**

```
Input: dictionary = ["cat","bat","rat"], sentence = "the cattle was rattled by the battery"
Output: "the cat was rat by the bat"

```

**Example 2:**

```
Input: dictionary = ["a","b","c"], sentence = "aadsfasf absbs bbab cadsfafs"
Output: "a a b c"

```

**Constraints:**

- `1 <= dictionary.length <= 1000`
- `1 <= dictionary[i].length <= 100`
- `dictionary[i]` consists of only lower-case letters.
- `1 <= sentence.length <= 106`
- `sentence` consists of only lower-case letters and spaces.
- The number of words in `sentence` is in the range `[1, 1000]`
- The length of each word in `sentence` is in the range `[1, 1000]`
- Every two consecutive words in `sentence` will be separated by exactly one space.
- `sentence` does not have leading or trailing spaces.

```java
class Solution {
    public String replaceWords(List<String> dictionary, String sentence) {
        Collections.sort(dictionary);
        StringBuilder sb = new StringBuilder();
        String[] sArr = sentence.split(" ");

        for(String s : sArr) {
            String tmp = "";
            for(String s1 : dictionary) {
                if(s.startsWith(s1)) {
                    tmp = s1;
                    break;
                }
            }
            if("".equals(tmp)) 
                sb.append(s).append(" ");
            else 
                sb.append(tmp).append(" ");
        }
        return sb.deleteCharAt(sb.length() - 1).toString();
    }
}
```

```java
class Solution {
    public String replaceWords(List<String> dictionary, String sentence) {
        TrieNode root = new TrieNode();
        StringBuilder sb = new StringBuilder();
        // 先做出trie
        for(String s : dictionary) {
            TrieNode insertTridNode = root;// root指標不動
            for(int i = 0; i < s.length(); i++){
                char c = s.charAt(i);//當前字母
                if(insertTridNode.children[c - 'a'] == null){
                    insertTridNode.children[c- 'a'] = new TrieNode();//給定當前結點val
                }
                insertTridNode = insertTridNode.children[c - 'a'];//到子node
            }
            insertTridNode.last = true;
        }
        // 搜尋
        String[] sentences = sentence.split(" ");
        for(String word : sentences) {
            TrieNode searchTrieNode = root;
            String tmp = "";
            for(int i = 0; i < word.length(); i++){
                char c = word.charAt(i);
                if(searchTrieNode.children[c - 'a'] == null){
                    tmp = word;
                    break;
                } else if(searchTrieNode.children[c - 'a'].last) {
                    tmp = word.substring(0, i + 1);
                    break;
                }
                else 
                    searchTrieNode = searchTrieNode.children[c - 'a'];//到子node
            }
            if("".equals(tmp)) 
                sb.append(word).append(" ");
            else 
                sb.append(tmp).append(" ");
        }
        return sb.deleteCharAt(sb.length() - 1).toString();
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