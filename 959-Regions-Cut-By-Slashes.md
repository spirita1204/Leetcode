# 959. Regions Cut By Slashes

Data structure: Union Find
Difficulty: Medium++

Medium

Topics

Companies

An `n x n` grid is composed of `1 x 1` squares where each `1 x 1` square consists of a `'/'`, `'\'`, or blank space `' '`. These characters divide the square into contiguous regions.

Given the grid `grid` represented as a string array, return *the number of regions*.

Note that backslash characters are escaped, so a `'\'` is represented as `'\\'`.

**Example 1:**

![https://assets.leetcode.com/uploads/2018/12/15/1.png](https://assets.leetcode.com/uploads/2018/12/15/1.png)

```
Input: grid = [" /","/ "]
Output: 2

```

**Example 2:**

![https://assets.leetcode.com/uploads/2018/12/15/2.png](https://assets.leetcode.com/uploads/2018/12/15/2.png)

```
Input: grid = [" /","  "]
Output: 1

```

**Example 3:**

![https://assets.leetcode.com/uploads/2018/12/15/4.png](https://assets.leetcode.com/uploads/2018/12/15/4.png)

```
Input: grid = ["/\\","\\/"]
Output: 5
Explanation:Recall that because \ characters are escaped, "\\/" refers to \/, and "/\\" refers to /\.

```

**Constraints:**

- `n == grid.length == grid[i].length`
- `1 <= n <= 30`
- `grid[i][j]` is either `'/'`, `'\'`, or `' '`.

```java
class Solution {
    public int regionsBySlashes(String[] grid) {
        int res = 1; 
        int row = grid.length;
        int col = grid[0].length();
        UnionFind unionFind = new UnionFind((row + 1) * (col + 1));
        // 先將外框union
        for (int i = 0; i <= row; i++) {
            for (int j = 0; j <= col; j++) {
                if (i > 0 && (j == 0 || j == col))
                    unionFind.unite((i - 1) * (col + 1) + j, i * (col + 1) + j); // 與上方相鄰點相連
                if (j > 0 && (i == 0 || i == row)) 
                    unionFind.unite(i * (col + 1) + (j - 1), i * (col + 1) + j); // 與左方相鄰點相連
            }
        }
        // 開始遍歷組合
        for (int i = 0; i < row; i++) {
            String s = grid[i];
            for (int j = 0; j < col; j++) {
                char ch = s.charAt(j);
                if ('/' == ch) {// h從 (x+1,y)連到(x+1,y)
                    int p1 = unionFind.findComponent(i * (row + 1) + j + 1);
                    int p2 = unionFind.findComponent((i + 1) * (row + 1) + j);
                    res += (!unionFind.unite(p1, p2)) ? 1: 0;// 已相連 拉出線必產生空間
                } else if ('\\' == ch) {// "\" 從(x,y)連到(x+1,y+1)
                    int p1 = unionFind.findComponent(i * (row + 1) + j);
                    int p2 = unionFind.findComponent((i + 1) * (row + 1) + (j + 1));
                    res += (!unionFind.unite(p1, p2)) ? 1: 0;
                } else {}// 空不處理
            }
        }
        return res;
    }
}

class UnionFind {
    int[] component;
    int distinctComponents;

    public UnionFind(int n) {
        component = new int[n + 1];
        for (int i = 0; i <= n; i++) {
            component[i] = i;
        } // {0,1,2,3,4}
        distinctComponents = n;// 4
    }

    // unite. For example, if previously we have component {0, 4, 4, 4, 4, 6, 7, 7},
    // then invoke this method with a=1, b=5, then after invoke, {0, 4, 4, 4, 5, 7,
    // 7, 7}
    public boolean unite(int a, int b) {
        if (findComponent(a) != findComponent(b)) {
            component[findComponent(a)] = b;
            distinctComponents--;
            return true;
        }
        return false;// 已經相連
    }

    // find and change component
    // for example, if previously we have component: {0, 2, 3, 4, 4, 6, 7, 7}, then
    // after invoke this method with a=1, the component become {0, 4, 4, 4, 4, 6, 7,
    // 7}
    // 找到 input 節點的 root ，可以藉此確定 input 節點屬於哪一個子集
    public int findComponent(int a) {
        if (component[a] != a) {
            component[a] = findComponent(component[a]);
        }
        return component[a];
    }

    // 是否使用n-1條邊
    private boolean united() {
        return distinctComponents == 1;
    }
}
```