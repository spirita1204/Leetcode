# 79. Word Search

Methods: DFS
Difficulty: Medium

Given an `m x n` grid of characters `board` and a string `word`, return `true` *if* `word` *exists in the grid*.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/11/04/word2.jpg](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg](https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
Output: true

```

**Example 3:**

![https://assets.leetcode.com/uploads/2020/10/15/word3.jpg](https://assets.leetcode.com/uploads/2020/10/15/word3.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
Output: false

```

**Constraints:**

- `m == board.length`
- `n = board[i].length`
- `1 <= m, n <= 6`
- `1 <= word.length <= 15`
- `board` and `word` consists of only lowercase and uppercase English letters.

**Follow up:** Could you use search pruning to make your solution faster with a larger `board`?

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        /*Find word's first letter.  Then call method to check it's surroundings */
        for(int r = 0; r < board.length; r++){
            for(int c = 0; c < board[0].length; c++){
                if(board[r][c] == word.charAt(0) && dfs(board,word,0,r,c))
                    return true;
            }
        }
        return false;
    }
    public boolean dfs(char[][] board, String word, int start, int r, int c){
        if(start >= word.length()){
            return true;
        }
        //out of bound 
        if(r < 0 || c < 0 || r >= board.length || c >= board[0].length || board[r][c] == '0'){
            return false;
        }
        //value not same
        if(board[r][c] != word.charAt(start)){
            return false;
        }
        //避免走重複(回頭)
        char temp = board[r][c];
        board[r][c] = '0';
        /* recursion on all 4 sides for next letter, if works: return true */
        if(dfs(board,word,start+1,r+1,c) ||
            dfs(board,word,start+1,r-1,c) ||
            dfs(board,word,start+1,r,c+1) ||
            dfs(board,word,start+1,r,c-1))
            return true;
        //當下一輪要變回來
        board[r][c] = temp;
        return false;
    }
}
```

不能用bfs會有問題 如下

```java
class Solution {
    public boolean exist(char[][] board, String word) {//bfs 同1162概念
        Queue<int[]> q = new ArrayDeque<>();
        int wordPointer = 1;
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[0].length; j++){
                if(board[i][j] == word.charAt(0)){//將代表字首放入q
                    q.offer(new int[]{i, j});
                    board[i][j] = '1';
                    System.out.println("add"+i+"&"+j);
                }
            }
        }
        int[][] dirs = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};//四個方向
        while(!q.isEmpty()){
            int size = q.size();//定義當前同一波數量
            while(size-- > 0){//掃過同一階層
                int[] now = q.poll();
                for(int[] e : dirs){
                    int i = now[0] + e[0];
                    int j = now[1] + e[1];
                    System.out.println("ori"+i+"&"+j);
                    if(i >= 0 && j >= 0 && i < board.length && j < board[0].length && board[i][j] != '1'){//沒超出邊界
                        System.out.println("in"+i+"&"+j);
                        if(wordPointer < word.length() && board[i][j] == word.charAt(wordPointer)){//當等於下個元素 取出丟入q
                            q.offer(new int[]{i, j});
                            System.out.println("add"+i+"&"+j);
                            board[i][j] = '1';//走過 替換成1
                        }
                    }  
                }
            }
            wordPointer++;
        }
        System.out.print(wordPointer);
        return (wordPointer > word.length())? true : false;
    }
}
```