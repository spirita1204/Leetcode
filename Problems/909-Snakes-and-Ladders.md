# 909. Snakes and Ladders

Methods: BFS
Difficulty: Medium

You are given an `n x n` integer matrix `board` where the cells are labeled from `1` to `n2` in a [**Boustrophedon style**](https://en.wikipedia.org/wiki/Boustrophedon) starting from the bottom left of the board (i.e. `board[n - 1][0]`) and alternating direction each row.

You start on square `1` of the board. In each move, starting from square `curr`, do the following:

- Choose a destination square `next` with a label in the range `[curr + 1, min(curr + 6, n2)]`.
    - This choice simulates the result of a standard **6-sided die roll**: i.e., there are always at most 6 destinations, regardless of the size of the board.
- If `next` has a snake or ladder, you **must** move to the destination of that snake or ladder. Otherwise, you move to `next`.
- The game ends when you reach the square `n2`.

A board square on row `r` and column `c` has a snake or ladder if `board[r][c] != -1`. The destination of that snake or ladder is `board[r][c]`. Squares `1` and `n2` do not have a snake or ladder.

Note that you only take a snake or ladder at most once per move. If the destination to a snake or ladder is the start of another snake or ladder, you do **not** follow the subsequent snake or ladder.

- For example, suppose the board is `[[-1,4],[-1,3]]`, and on the first move, your destination square is `2`. You follow the ladder to square `3`, but do **not** follow the subsequent ladder to `4`.

Return *the least number of moves required to reach the square* `n2`*. If it is not possible to reach the square, return* `-1`.

**Example 1:**

![https://assets.leetcode.com/uploads/2018/09/23/snakes.png](https://assets.leetcode.com/uploads/2018/09/23/snakes.png)

```
Input: board = [[-1,-1,-1,-1,-1,-1],[-1,-1,-1,-1,-1,-1],[-1,-1,-1,-1,-1,-1],[-1,35,-1,-1,13,-1],[-1,-1,-1,-1,-1,-1],[-1,15,-1,-1,-1,-1]]
Output: 4
Explanation:
In the beginning, you start at square 1 (at row 5, column 0).
You decide to move to square 2 and must take the ladder to square 15.
You then decide to move to square 17 and must take the snake to square 13.
You then decide to move to square 14 and must take the ladder to square 35.
You then decide to move to square 36, ending the game.
This is the lowest possible number of moves to reach the last square, so return 4.

```

**Example 2:**

```
Input: board = [[-1,-1],[-1,3]]
Output: 1

```

**Constraints:**

- `n == board.length == board[i].length`
- `2 <= n <= 20`
- `board[i][j]` is either `1` or in the range `[1, n2]`.
- The squares labeled `1` and `n2` do not have any ladders or snakes.

```java
//problem 909
class Solution {
    public int snakesAndLadders(int[][] board) {
        //https://www.youtube.com/watch?v=0psTRx1FxPQ
        //座標對應2d矩陣位置
        /*
        1.
        //row = n-(num-1)/n-1
        //column = odd(->) = (num-1)%n
        //         even(<-) = n-(num-1)%n-1
        2.
        有cycle
        ex : 1 1 -1
             1 1  1
            -1 1  1
        都指向自己 就continue
        */
        if(board == null || board.length==0) return 0;
        int n = board.length;
        boolean[] visited = new boolean[n*n+1];
        int min = n*n;
        Queue<Integer> q = new ArrayDeque<>();//效能比arraylist好
        q.offer(1);
        int moves = 0;
        while(!q.isEmpty()){
            int qSize = q.size();//不然會一直進入第29行
            for(int i=0;i<qSize;i++){
                int cur = q.poll();
                if(cur == n*n) min = Math.min(min,moves);//走到終點
                for(int j=1;j<=6;j++){//6種走法 +1+2+3+4+5+6
                    int num = cur+j;
                    if(num > n*n) break;//當超出直接不做
                    int row = n-(num-1)/n-1;
                    int column = ((n-row)%2 != 0)? (num-1)%n : n-(num-1)%n-1;
                    //         判斷是偶數 還奇數
                    if(!visited[num]){//purning避免重複走
                        visited[num] = true;
                        if(board[row][column]==-1){//沒東西
                            q.offer(num);
                        }else{//梯子或蛇
                            q.offer(board[row][column]);
                        }
                    }
                }
            }   
            moves++;//走一步
        }
        return (min == n*n)? -1 : min;//[[1,1,-1],[1,1,1],[-1,1,1]] cycle情況
    }
    
}
```