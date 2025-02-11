# 289. Game of Life

Methods: Basic logic
Difficulty: Medium

[康威生命遊戲 - 維基百科，自由的百科全書](https://zh.wikipedia.org/zh-tw/康威生命游戏)

According to [Wikipedia's article](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life): "The **Game of Life**, also known simply as **Life**, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

The board is made up of an `m x n` grid of cells, where each cell has an initial state: **live** (represented by a `1`) or **dead** (represented by a `0`). Each cell interacts with its [eight neighbors](https://en.wikipedia.org/wiki/Moore_neighborhood) (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

1. Any live cell with fewer than two live neighbors dies as if caused by under-population.
2. Any live cell with two or three live neighbors lives on to the next generation.
3. Any live cell with more than three live neighbors dies, as if by over-population.
4. Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.

The next state is created by applying the above rules simultaneously to every cell in the current state, where births and deaths occur simultaneously. Given the current state of the `m x n` grid `board`, return *the next state*.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/12/26/grid1.jpg](https://assets.leetcode.com/uploads/2020/12/26/grid1.jpg)

```
Input: board = [[0,1,0],[0,0,1],[1,1,1],[0,0,0]]
Output: [[0,0,0],[1,0,1],[0,1,1],[0,1,0]]

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/12/26/grid2.jpg](https://assets.leetcode.com/uploads/2020/12/26/grid2.jpg)

```
Input: board = [[1,1],[1,0]]
Output: [[1,1],[1,1]]

```

**Constraints:**

- `m == board.length`
- `n == board[i].length`
- `1 <= m, n <= 25`
- `board[i][j]` is `0` or `1`.

**Follow up:**

- Could you solve it in-place? Remember that the board needs to be updated simultaneously: You cannot update some cells first and then use their updated values to update other cells.
- In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches upon the border of the array (i.e., live cells reach the border). How would you address these problems?

```java
class Solution {
    public void gameOfLife(int[][] board) {
        /*
        [2nd bit, 1st bit] = [next state, current state]
        - 00  dead (next) <- dead (current)
        - 01  dead (next) <- live (current)  
        - 10  live (next) <- dead (current)  
        - 11  live (next) <- live (current)

        To get the current state, simply do : board[i][j] & 1 做and運算
        To get the next state, simply do : board[i][j] >> 1 右移一位元 
        */
        if (board == null || board.length == 0) return;//null 空不用做
        int m = board.length, n = board[0].length;

        for(int i =  0; i < m; i++){
            for(int j = 0; j < n; j++){
                int aliveNeighborsNums = aliveNeighbors(board, i, j, m, n);//計算當前節點 neighbors alive 個數
                
                if((board[i][j] & 1) == 1){//alive situation = 1 // bit operator要括號
                    if(aliveNeighborsNums < 2){}//當前變死亡 nextState = 0 //不用做動作 01
                    if(aliveNeighborsNums == 2 || aliveNeighborsNums == 3)//維持現狀 nextState = currentState //11
                        board[i][j] = 3; 
                    if(aliveNeighborsNums > 3){}// over-population nextState = 0 //不用做用 01  
                }else{//die situation
                    if(aliveNeighborsNums == 3)// reproduction nextState = 1
                        board[i][j] = 2;
                }
            }
        }
        for(int i =  0; i < m; i++){
            for(int j = 0; j < n; j++){
                board[i][j] = board[i][j] >> 1;//跳轉到nextState 
            }
        }
    }
    public int aliveNeighbors(int[][] board, int i, int j, int m, int n){//存活鄰居個數 (i, j)座標
        int nums = 0;
        int[][] dirs = {{-1, -1}, {-1, 0}, {0, -1}, {1, 0}, {0, 1}, {-1, 1}, {1, -1}, {1,1}};//周圍方位
        for(int[] dir : dirs){
            int x = dir[0] + i;
            int y = dir[1] + j;
            if(x >= 0 && x < m && y >= 0 && y < n)//當未越界
                if((board[x][y] & 1) == 1) nums++;
        }
        return nums;
    }
}289. Game of Life289. Game of Life
```