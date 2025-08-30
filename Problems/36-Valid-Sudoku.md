# 36. Valid Sudoku  

  Data Structure: Hash Table </br> Difficulty: Medium </br> </br>Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:   

1. Each row must contain the digits `1-9` without repetition.
1. Each column must contain the digits `1-9` without repetition.
1. Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.
**Note:**

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.
**Example 1:**

![Image](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

```plain text
Input: board =
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```

**Example 2:**

```plain text
Input: board =
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: false
Explanation: Same as Example 1, except with the5 in the top left corner being modified to8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

**Constraints:**

- `board.length == 9`
- `board[i].length == 9`
- `board[i][j]` is a digit `1-9` or `'.'`.
```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        for (int i = 0; i < 9; i++) {
            if (leftRightValid(i, 0, board) == false || topDownValid(0, i, board) == false
                    || cubeValid(i, 0, board) == false) {
                return false;
            }
        }
        return true;

    }

    public boolean leftRightValid(int x, int y, char[][] board) {
        HashSet<Character> rows = new HashSet<Character>();
        for (int i = 0; i < board.length; i++) {
            if (board[x][i] != '.' && !rows.add(board[x][i])) {
                return false;
            }
        }
        return true;

    }

    public boolean topDownValid(int x, int y, char[][] board) {
        HashSet<Character> columns = new HashSet<Character>();
        for (int i = 0; i < board.length; i++) {
            if (board[i][y] != '.' && !columns.add(board[i][y])) {
                return false;
            }
        }
        return true;
    }

    public boolean cubeValid(int x, int y, char[][] board) {
        HashSet<Character> cubes = new HashSet<Character>();
        for (int i = 0; i < 9; i++) {
            if (board[(x / 3) * 3 + i / 3][(x % 3) * 3 + i % 3] != '.'
                    && !cubes.add(board[(x / 3) * 3 + i / 3][(x % 3) * 3 + i % 3])) {
                return false;
            }
        }
        return true;
    }
}
```

