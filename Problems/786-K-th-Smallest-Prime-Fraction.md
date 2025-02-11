# 786. K-th Smallest Prime Fraction

Data structure: Heap
Difficulty: Medium

![Untitled](Untitled%2011.png)

You are given a sorted integer array `arr` containing `1` and **prime** numbers, where all the integers of `arr` are unique. You are also given an integer `k`.

For every `i` and `j` where `0 <= i < j < arr.length`, we consider the fraction `arr[i] / arr[j]`.

Return *the* `kth` *smallest fraction considered*. Return your answer as an array of integers of size `2`, where `answer[0] == arr[i]` and `answer[1] == arr[j]`.

**Example 1:**

```
Input: arr = [1,2,3,5], k = 3
Output: [2,5]
Explanation: The fractions to be considered in sorted order are:
1/5, 1/3, 2/5, 1/2, 3/5, and 2/3.
The third fraction is 2/5.

```

**Example 2:**

```
Input: arr = [1,7], k = 1
Output: [1,7]

```

**Constraints:**

- `2 <= arr.length <= 1000`
- `1 <= arr[i] <= 3 * 104`
- `arr[0] == 1`
- `arr[i]` is a **prime** number for `i > 0`.
- All the numbers of `arr` are **unique** and sorted in **strictly increasing** order.
- `1 <= k <= arr.length * (arr.length - 1) / 2`

**Follow up:**

Can you solve the problem with better than

```
O(n2)
```

complexity?

### PriorityQueue N^2解法 easy

```java
class Solution {
    public int[] kthSmallestPrimeFraction(int[] arr, int k) {
        // Queue<int[]> q = new PriorityQueue<>((a, b) -> ((double)(a[0] / a[1]) - (double)(b[0] / b[1])));
        Queue<int[]> q = new PriorityQueue<>((a, b) -> Double.compare((double)a[0] / a[1], (double)b[0] / b[1]));

        for (int i = 0; i < arr.length; i++) {
            for (int j = i + 1; j < arr.length; j++) {
                q.offer(new int[] {arr[i] , arr[j]});
            }
        }
        while (k-- > 1) {
            q.poll();
        }
        return q.poll();
    }
}
```

### BS NLogN解法Hard

```java
class Solution {
    public int[] kthSmallestPrimeFraction(int[] arr, int k) {
        /** solution2 BinarySearch*/    
        int n = arr.length;
        double l = 0;
        double r = 1;
        while(l < r) {
            double mid = (l + r) / 2.;
            double max = 0; // 存當前選擇條件中最大->要輸出那個 
            int total = 0; // 小於mid 個數
            int p = 0, q = 0; // 最大x, y座標
            int j = 1; // y

            for(int i = 0; i < n - 1; i++) {
                while(j < n && arr[i] > mid* arr[j]) j++;// 找到第一個小於m的j座標
                total += (n - j);// 計算小於mid有幾個
                if(n == j) break;
                double f = (double)arr[i] / arr[j];
                if(f > max) {
                    max = f;
                    p = i;
                    q = j;
                }
            }
            if(total == k) // 剛好一陽
                return new int[] {arr[p], arr[q]};
            if(total > k) 
                r = mid;// 不用加1 減1
            else 
                l = mid;
        }
    return new int[]{};
    }
}
```