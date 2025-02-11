# 221. Maximal Square

Methods: DP
Difficulty: Medium

[https://www.youtube.com/watch?v=vkFUB--OYy0](https://www.youtube.com/watch?v=vkFUB--OYy0)

Given an `m x n` binary `matrix` filled with `0`'s and `1`'s, *find the largest square containing only* `1`'s *and return its area*.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/11/26/max1grid.jpg](https://assets.leetcode.com/uploads/2020/11/26/max1grid.jpg)

```
Input: matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
Output: 4

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/11/26/max2grid.jpg](https://assets.leetcode.com/uploads/2020/11/26/max2grid.jpg)

```
Input: matrix = [["0","1"],["1","0"]]
Output: 1

```

**Example 3:**

```
Input: matrix = [["0"]]
Output: 0
```

![Untitled](Untitled%205.png)

![Untitled](Untitled%206.png)

O(n^3)

```java
class Solution {
    public int maximalSquare(char[][] matrix) {
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
                for(int k = Math.min(m-i+1,n-j+1);k>0;k--){//枚舉正方形大小
                    int sum = sums[i+k-1][j+k-1]
                             -sums[i+k-1][j-1]
                             -sums[i-1][j+k-1]
                             +sums[i-1][j-1];
                    if(sum == k*k){
                        ans = Math.max(ans,sum);
                        break;
                    }
                }
            }
        }
        return ans;
    }
}
```

![Untitled](Untitled%207.png)

![Untitled](Untitled%208.png)