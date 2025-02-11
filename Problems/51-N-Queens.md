# 51. N-Queens

Methods: DFS
Data structure: Set
Difficulty: Hard

Hard

Topics

Companies

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return *all distinct solutions to the **n-queens puzzle***. You may return the answer in **any order**.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/11/13/queens.jpg](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

```
Input: n = 4
Output: [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
Explanation: There exist two distinct solutions to the 4-queens puzzle as shown above

```

**Example 2:**

```
Input: n = 1
Output: [["Q"]]

```

**Constraints:**

- `1 <= n <= 9`

```java
public class Solution {
    private Set<Integer> col = new HashSet<Integer>();// 橫
    private Set<Integer> diag1 = new HashSet<Integer>();// 對角線
    private Set<Integer> diag2 = new HashSet<Integer>();// 對角線

    public List<List<String>> solveNQueens(int n) {
        List<List<String>> res = new ArrayList<List<String>>();
        dfs(res, new ArrayList<String>(), 0, n);

        return res;
    }

    private void dfs(List<List<String>> res, List<String> list, int row, int n) {
        if (row == n) {
            res.add(new ArrayList<String>(list));
            return;
        }
        for (int j = 0; j < n; j++) {
            if (col.contains(j) || diag1.contains(row + j) || diag2.contains(row - j))
                continue;

            char[] charArray = new char[n];
            Arrays.fill(charArray, '.');
            charArray[j] = 'Q';
            String rowString = new String(charArray);
           
            list.add(rowString);
            col.add(j);
            diag1.add(row + j);
            diag2.add(row - j);

            dfs(res, list, row + 1, n);
          
            list.remove(list.size() - 1);
            col.remove(j);
            diag1.remove(row + j);
            diag2.remove(row - j);
        }
    }
}
```