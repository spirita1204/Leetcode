# 130. Surrounded Regions

Methods: BFS
Difficulty: Medium

**Medium**

6.9K

1.5K

Companies

Given an `m x n` matrix `board` containing `'X'` and `'O'`, *capture all regions that are 4-directionally surrounded by* `'X'`.

A region is **captured** by flipping all `'O'`s into `'X'`s in that surrounded region.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/02/19/xogrid.jpg](https://assets.leetcode.com/uploads/2021/02/19/xogrid.jpg)

```
Input: board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
Output: [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
Explanation: Notice that an 'O' should not be flipped if:
- It is on the border, or
- It is adjacent to an 'O' that should not be flipped.
The bottom 'O' is on the border, so it is not flipped.
The other three 'O' form a surrounded region, so they are flipped.

```

**Example 2:**

```
Input: board = [["X"]]
Output: [["X"]]

```

**Constraints:**

- `m == board.length`
- `n == board[i].length`
- `1 <= m, n <= 200`
- `board[i][j]` is `'X'` or `'O'`.

```java
class Solution {
    public void solve(char[][] board) {
        int[] dirs = {0, 1, 0, -1, 0};
        // Traversing on 1st row
        for(int j= 0; j< board[0].length; j++){
            // If we found an 'O' on border, we need to make all its connected 'O's to '1's.
            if(board[0][j]=='O') bfs(board, 0, j, dirs);   
        }
        // Traversing on last row
        for(int j= 0; j< board[0].length; j++){
            if(board[board.length-1][j]=='O') bfs(board, board.length-1, j, dirs);
        }
        // Traversing on first column
        for(int i= 0; i< board.length; i++){
            if(board[i][0]=='O') bfs(board, i, 0, dirs);
        }
        // Traversing on last column
        for(int i= 0; i< board.length; i++){
            if(board[i][board[0].length-1]=='O') bfs(board, i, board[0].length-1, dirs);
        }
        // Traverse the grid again and perform step 2
        for(int i= 0; i< board.length; i++){
            for(int j= 0; j< board[0].length; j++){
                if(board[i][j] == 'O') board[i][j]='X';
                else if(board[i][j] == '1') board[i][j]='O';     
            }
        }
    }
    public void bfs(char[][] board, int i, int j, int[] dirs){
        Queue<int[]> q = new LinkedList<>();
        q.offer(new int[]{i, j});
        board[i][j] = '1';
        
        while(!q.isEmpty()){
            int[] node = q.poll();

            for(int d = 0; d< dirs.length - 1; d++){
                int x = node[0] + dirs[d];
                int y = node[1] + dirs[d + 1];

                if(x >= 0 && x < board.length && y >= 0 && y < board[0].length){
                    if(board[x][y] == 'O'){
                        board[x][y] = '1';
                        q.offer(new int[]{x, y});
                    }
                }
            }
        }
    }
}
```