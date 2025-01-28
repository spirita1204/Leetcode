# 1337. The K Weakest Rows in a Matrix

Methods: Basic logic
Difficulty: Easy

**Easy**

3.2K

189

Companies

You are given an `m x n` binary matrix `mat` of `1`'s (representing soldiers) and `0`'s (representing civilians). The soldiers are positioned **in front** of the civilians. That is, all the `1`'s will appear to the **left** of all the `0`'s in each row.

A row `i` is **weaker** than a row `j` if one of the following is true:

- The number of soldiers in row `i` is less than the number of soldiers in row `j`.
- Both rows have the same number of soldiers and `i < j`.

Return *the indices of the* `k` ***weakest** rows in the matrix ordered from weakest to strongest*.

**Example 1:**

```
Input: mat =
[[1,1,0,0,0],
 [1,1,1,1,0],
 [1,0,0,0,0],
 [1,1,0,0,0],
 [1,1,1,1,1]],
k = 3
Output: [2,0,3]
Explanation:
The number of soldiers in each row is:
- Row 0: 2
- Row 1: 4
- Row 2: 1
- Row 3: 2
- Row 4: 5
The rows ordered from weakest to strongest are [2,0,3,1,4].

```

**Example 2:**

```
Input: mat =
[[1,0,0,0],
 [1,1,1,1],
 [1,0,0,0],
 [1,0,0,0]],
k = 2
Output: [0,2]
Explanation:
The number of soldiers in each row is:
- Row 0: 1
- Row 1: 4
- Row 2: 1
- Row 3: 1
The rows ordered from weakest to strongest are [0,2,3,1].

```

**Constraints:**

- `m == mat.length`
- `n == mat[i].length`
- `2 <= n, m <= 100`
- `1 <= k <= m`
- `matrix[i][j]` is either 0 or 1.

```java
class Solution {
    public int[] kWeakestRows(int[][] mat, int k) {
        int[] res = new int[mat.length];
        //用來處理數字照prior出來用 (並實作comparator) 當第一位相同 確認第二位大小
        Queue<int[]> pq = new PriorityQueue<>((a, b) -> (a[0] != b[0]) ? a[0] - b[0] : a[1] - b[1]);
        
        for(int i = 0; i< mat.length; i++){
            int left = 0;
            int right = mat[0].length - 1;
            while(left <= right){
                int mid = left + (right - left)/2;
                if(mat[i][mid] == 1){
                    left = mid + 1;
                }else{
                    right = mid -1;
                }
            }
            res[i] = left;
        }
        //對arr作優先排序 2,4,1,2,5 -> 2,0,3,1,4
        //(2, 0),(4, 1),(1, 2),(2, 3),(5, 4)依據前者排序
        for(int i = 0; i< res.length; i++) pq.offer( new int[]{res[i], i} );
        //取出
        for(int i = 0; i< res.length; i++) res[i] = pq.poll()[1];

        return Arrays.copyOfRange(res, 0, k);
    }
}
```