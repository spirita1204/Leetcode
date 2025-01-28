# 85. Maximal Rectangle

Methods: DP
Difficulty: Hard

Given a `rows x cols` binary `matrix` filled with `0`'s and `1`'s, find the largest rectangle containing only `1`'s and return *its area*.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/09/14/maximal.jpg](https://assets.leetcode.com/uploads/2020/09/14/maximal.jpg)

```
Input: matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
Output: 6
Explanation: The maximal rectangle is shown in the above picture.

```

**Example 2:**

```
Input: matrix = [["0"]]
Output: 0

```

**Example 3:**

```
Input: matrix = [["1"]]
Output: 1

```

**Constraints:**

- `rows == matrix.length`
- `cols == matrix[i].length`
- `1 <= row, cols <= 200`
- `matrix[i][j]` is `'0'` or `'1'`.

```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;
        int[][] sums = new int[m+1][n+1];
        for(int i = 1;i<=m;i++){
            for(int j = 1;j<=n;j++){
                sums[i][j] = matrix[i-1][j-1]-'0'
                            + sums[i-1][j]
                            + sums[i][j-1]
                            - sums[i-1][j-1];
            }
        }
        for(int[] i : sums){
            for(int j: i) {
                System.out.print(j);
            }
            System.out.println("");
        }
        int ans = 0;
        for(int i = 1;i<=m;i++){//左上角初始點
            for(int j = 1;j<=n;j++){//左上角初始點
                for(int k = m-i+1;k>0;k--){//枚舉長方形長
                    for(int l = n-j+1;l>0;l--){//枚舉長方形寬
                        int sum = sums[i+k-1][j+l-1]
                                -sums[i+k-1][j-1]
                                -sums[i-1][j+l-1]
                                +sums[i-1][j-1];
                        if(sum == k*l){
                            ans = Math.max(ans,sum);
                            break;
                        }
                    }
                }
            }
        }
        return ans;       
    }
}
```