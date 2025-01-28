# 52. N-Queens II

Methods: DFS
Data structure: Set
Difficulty: Hard

Hard

Topics

Companies

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return *the number of distinct solutions to the **n-queens puzzle***.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/11/13/queens.jpg](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

```
Input: n = 4
Output: 2
Explanation: There are two distinct solutions to the 4-queens puzzle as shown.

```

**Example 2:**

```
Input: n = 1
Output: 1

```

**Constraints:**

- `1 <= n <= 9`

```java
class Solution {
    private Set<Integer> col = new HashSet<Integer>();// 橫
    private Set<Integer> diag1 = new HashSet<Integer>();// 對角線
    private Set<Integer> diag2 = new HashSet<Integer>();// 對角線
    int res = 0;
    public int totalNQueens(int n) {
        dfs(new ArrayList<String>(), 0, n);

        return res;
    }
    private void dfs(List<String> list, int row, int n) {
        if (row == n) {
            res++;
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

            dfs(list, row + 1, n);
          
            list.remove(list.size() - 1);
            col.remove(j);
            diag1.remove(row + j);
            diag2.remove(row - j);
        }
    }
}
```