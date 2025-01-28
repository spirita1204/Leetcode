# 378. Kth Smallest Element in a Sorted Matrix

Methods: Binary Search
Data structure: Heap
Difficulty: Medium

Medium

Topics

Companies

Given an `n x n` `matrix` where each of the rows and columns is sorted in ascending order, return *the* `kth` *smallest element in the matrix*.

Note that it is the `kth` smallest element **in the sorted order**, not the `kth` **distinct** element.

You must find a solution with a memory complexity better than `O(n2)`.

**Example 1:**

```
Input: matrix = [[1,5,9],[10,11,13],[12,13,15]], k = 8
Output: 13
Explanation: The elements in the matrix are [1,5,9,10,11,12,13,13,15], and the 8th smallest number is 13

```

**Example 2:**

```
Input: matrix = [[-5]], k = 1
Output: -5

```

**Constraints:**

- `n == matrix.length == matrix[i].length`
- `1 <= n <= 300`
- `109 <= matrix[i][j] <= 109`
- All the rows and columns of `matrix` are **guaranteed** to be sorted in **non-decreasing order**.
- `1 <= k <= n2`

**Follow up:**

- Could you solve the problem with a constant memory (i.e., `O(1)` memory complexity)?
- Could you solve the problem in `O(n)` time complexity? The solution may be too advanced for an interview but you may find reading [this paper](http://www.cse.yorku.ca/~andy/pubs/X+Y.pdf) fun.

```
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        // solution1 heap從左手邊 開始往右掃
        // int length = matrix[0].length;  

        // PriorityQueue<int[]> pq = new PriorityQueue<>((a, b)-> a[0]- b[0]);// 存(值, x標, y標)

        // for(int i = 0; i< matrix.length; i++) {
        //     pq.add(new int[]{matrix[i][0], i, 0});
        // }
        // while(k--> 0) {
        //     int[] min = pq.poll();
        //     if(k == 0) return min[0];// 當找到第k個小 輸出
        //     if(min[2]+ 1< length) {
        //         pq.add(new int[]{matrix[min[1]][min[2]+ 1], min[1], min[2]+ 1});
        //     }
        // }
        // return -1;

        // solution2 bs
        int height = matrix.length;  
        int length = matrix[0].length;  

        int left = matrix[0][0];
        int right = matrix[height-1][length-1];
        
        while(left <= right) {
            int mid = left + (right - left) / 2;
            int count = countSmallerOrEqual(matrix, mid);
            if(count >= k) {
                right = mid - 1;
            }else {
                left = mid + 1;
            }
        }
        return left;
    }

    private int countSmallerOrEqual(int[][] matrix, int mid) {// 從左下角往右上角掃
        int height = matrix.length;  
        int count = 0;
        int x = height - 1, y = 0;
        while(x >= 0 && y < height) {
            if(matrix[x][y] <= mid) {
                count += (x + 1);
                y++;// 往右移
            }else {
                x--;
            }
        }
        return count;
    }
}
```