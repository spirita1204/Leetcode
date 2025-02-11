# 127. Word Ladder

Methods: BFS
Data structure: Set
Difficulty: Hard

Hard

Topics

Companies

A **transformation sequence** from word `beginWord` to word `endWord` using a dictionary `wordList` is a sequence of words `beginWord -> s1 -> s2 -> ... -> sk` such that:

- Every adjacent pair of words differs by a single letter.
- Every `si` for `1 <= i <= k` is in `wordList`. Note that `beginWord` does not need to be in `wordList`.
- `sk == endWord`

Given two words, `beginWord` and `endWord`, and a dictionary `wordList`, return *the **number of words** in the **shortest transformation sequence** from* `beginWord` *to* `endWord`*, or* `0` *if no such sequence exists.*

**Example 1:**

```
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5
Explanation: One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long.

```

**Example 2:**

```
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
Output: 0
Explanation: The endWord "cog" is not in wordList, therefore there is no valid transformation sequence.

```

**Constraints:**

- `1 <= beginWord.length <= 10`
- `endWord.length == beginWord.length`
- `1 <= wordList.length <= 5000`
- `wordList[i].length == beginWord.length`
- `beginWord`, `endWord`, and `wordList[i]` consist of lowercase English letters.
- `beginWord != endWord`
- All the words in `wordList` are **unique**.

## **Time Limit Exceeded**

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Queue<String> q = new LinkedList<>();
        Set<String> s = new HashSet<>();// 避免重複遍歷
        q.offer(beginWord);
        s.add(beginWord);

        int res = 1;
        while(!q.isEmpty()) {
            int size = q.size();
            while(size-- > 0){
                String str = q.poll();
                if(endWord.equals(str)) return res;// 當找到時輸出
                for(String end: wordList) {
                    if(diffStrNum(str, end) == 1 && !s.contains(end)) {
                        q.offer(end);
                        s.add(str);
                    }
                }
            }   
            res++;   
        }
        return 0;
    }
    private int diffStrNum(String startGene, String endGene) {
        int cnt = 0;
        for (int i = 0; i < startGene.length(); i++) {
            if (startGene.charAt(i) != endGene.charAt(i))
                cnt++;
        }
        return cnt;
    }
}
```

使用HashSet優化

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Queue<String> q = new LinkedList<>();
        Set<String> s = new HashSet<>(wordList);// 新增 修改 刪除都是O(1) hash
        
        q.offer(beginWord);
        int res = 1;

        while(!q.isEmpty()) {
            int size = q.size();
            while(size-- > 0){
                String str = q.poll();
                // 對str每一位 尋找a~z轉換 判斷是否在set中
                for(int i = 0; i < str.length(); i++) {
                    char[] cArr = str.toCharArray();
                    for(char c = 'a'; c <= 'z'; c++) {
                        cArr[i] = c;
                        String tmp = new String(cArr);// 單獨改某一位
                        if(s.contains(tmp)) {
                            if(tmp.equals(endWord)) return res + 1;
                            q.offer(tmp);
                            s.remove(tmp);
                        }
                    }
                }
            }
            res++;   
        }
        return 0;
    }
}
```