# 37. Sudoku Solver  

  Methods: DFS </br> Difficulty: Hard </br> </br>Write a program to solve a Sudoku puzzle by filling the empty cells.

A sudoku solution must satisfy **all of the following rules**:

1. Each of the digits `1-9` must occur exactly once in each row.
1. Each of the digits `1-9` must occur exactly once in each column.
1. Each of the digits `1-9` must occur exactly once in each of the 9 `3x3` sub-boxes of the grid.  
The `'.'` character indicates empty cells.

**Example 1:**

![Image](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

```plain text
Input: board = [["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
Output: [["5","3","4","6","7","8","9","1","2"],["6","7","2","1","9","5","3","4","8"],["1","9","8","3","4","2","5","6","7"],["8","5","9","7","6","1","4","2","3"],["4","2","6","8","5","3","7","9","1"],["7","1","3","9","2","4","8","5","6"],["9","6","1","5","3","7","2","8","4"],["2","8","7","4","1","9","6","3","5"],["3","4","5","2","8","6","1","7","9"]]
Explanation: The input board is shown above and the only valid solution is shown below:
```

![Image](https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png)

**Constraints:**

- `board.length == 9`
- `board[i].length == 9`
- `board[i][j]` is a digit or `'.'`.
- It is **guaranteed** that the input board has only one solution.
```java
class Solution {
    public void solveSudoku(char[][] board) {
        backtracking(board, 0, 0);
    }

    private boolean backtracking(char[][] board, int row, int col) {
        if (row == board.length) // 最後一層+1 代表都填滿
            return true;
        if (col == board[0].length) // 最後一邊 換行
            return backtracking(board, row + 1, 0);
        if (board[row][col] != '.') // 有值 換下一位
            return backtracking(board, row, col + 1);
        
        for (char num = '1'; num <= '9'; num++) {
            if (isValid(board, row, col, num)) {
                board[row][col] = num;
                if (backtracking(board, row, col + 1)) 
                    return true;
                board[row][col] = '.';
            }
        }
        return false;
    }

    private boolean isValid(char[][] board, int row, int col, char num) {
        for (int i = 0; i < board.length; i++) {
            if (board[i][col] == num) // 直
                return false;
            
            if (board[row][i] == num) // 橫
                return false;
            
            int subgridRow = 3 * (row / 3) + i / 3; 
            int subgridCol = 3 * (col / 3) + i % 3;

            if (board[subgridRow][subgridCol] == num) // 子正方形
                return false;
        }
        return true;
    }
}
```

