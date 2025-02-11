# 1861. Rotating the Box

Methods: Basic logic

# [**1861. Rotating the Box**](https://leetcode.com/problems/rotating-the-box/)

Solved

Medium

Topics

Companies

Hint

You are given an `m x n` matrix of characters `box` representing a side-view of a box. Each cell of the box is one of the following:

- A stone `'#'`
- A stationary obstacle `'*'`
- Empty `'.'`

The box is rotated **90 degrees clockwise**, causing some of the stones to fall due to gravity. Each stone falls down until it lands on an obstacle, another stone, or the bottom of the box. Gravity **does not** affect the obstacles' positions, and the inertia from the box's rotation **does not** affect the stones' horizontal positions.

It is **guaranteed** that each stone in `box` rests on an obstacle, another stone, or the bottom of the box.

Return *an* `n x m` *matrix representing the box after the rotation described above*.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/04/08/rotatingtheboxleetcodewithstones.png](https://assets.leetcode.com/uploads/2021/04/08/rotatingtheboxleetcodewithstones.png)

```
Input: box = [["#",".","#"]]
Output: [["."],
         ["#"],
         ["#"]]

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/04/08/rotatingtheboxleetcode2withstones.png](https://assets.leetcode.com/uploads/2021/04/08/rotatingtheboxleetcode2withstones.png)

```
Input: box = [["#",".","*","."],
              ["#","#","*","."]]
Output: [["#","."],
         ["#","#"],
         ["*","*"],
         [".","."]]

```

**Example 3:**

![https://assets.leetcode.com/uploads/2021/04/08/rotatingtheboxleetcode3withstone.png](https://assets.leetcode.com/uploads/2021/04/08/rotatingtheboxleetcode3withstone.png)

```
Input: box = [["#","#","*",".","*","."],
              ["#","#","#","*",".","."],
              ["#","#","#",".","#","."]]
Output: [[".","#","#"],
         [".","#","#"],
         ["#","#","*"],
         ["#","*","."],
         ["#",".","*"],
         ["#",".","."]]

```

**Constraints:**

- `m == box.length`
- `n == box[i].length`
- `1 <= m, n <= 500`
- `box[i][j]` is either `'#'`, `'*'`, or `'.'`.
    
    ```java
    class Solution {
        public char[][] rotateTheBox(char[][] box) {
            int row = box.length;// 2 
            int col = box[0].length;// 4
            char[][] box2 = new char[col][row];
    
            for (int i = 0; i < row; i++) {// 遍歷
                int empty = col - 1;
                for (int j = col - 1; j >= 0; j--) {
                    if (box[i][j] == '*') {// 障礙
                        empty = j - 1;
                    }
                    if (box[i][j] == '#') {
                        box[i][j] = '.';
                        box[i][empty] = '#';
                        empty--;
                    }
                }
            }
            // 翻轉
            for (int i = 0; i < row; i++) {
                for (int j = 0; j < col; j++)
                    box2[j][row - i - 1] = box[i][j];
            }
    
            return box2;
        }
    }
    ```