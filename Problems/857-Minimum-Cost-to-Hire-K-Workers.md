# 857. Minimum Cost to Hire K Workers

Data structure: Heap
Difficulty: Hard

Hard

Topics

Companies

There are `n` workers. You are given two integer arrays `quality` and `wage` where `quality[i]` is the quality of the `ith` worker and `wage[i]` is the minimum wage expectation for the `ith` worker.

We want to hire exactly `k` workers to form a **paid group**. To hire a group of `k` workers, we must pay them according to the following rules:

1. Every worker in the paid group must be paid at least their minimum wage expectation.
2. In the group, each worker's pay must be directly proportional to their quality. This means if a worker’s quality is double that of another worker in the group, then they must be paid twice as much as the other worker.

Given the integer `k`, return *the least amount of money needed to form a paid group satisfying the above conditions*. Answers within `10-5` of the actual answer will be accepted.

**Example 1:**

```
Input: quality = [10,20,5], wage = [70,50,30], k = 2
Output: 105.00000
Explanation: We pay 70 to 0th worker and 35 to 2nd worker.

```

**Example 2:**

```
Input: quality = [3,1,10,10,1], wage = [4,8,2,2,7], k = 3
Output: 30.66667
Explanation: We pay 4 to 0th worker, 13.33333 to 2nd and 3rd workers separately.

```

**Constraints:**

- `n == quality.length == wage.length`
- `1 <= k <= n <= 104`
- `1 <= quality[i], wage[i] <= 104`

```java
class Solution {
    public double mincostToHireWorkers(int[] quality, int[] wage, int k) {
        // 7 2.5 6
        // 1.3 8 0.5 0.5 7
        int len = quality.length;
        double[][] workers = new double[len][2];// [cp, quality]
        double res = Double.MAX_VALUE;
        double qsum = 0;
        PriorityQueue<Double> pq = new PriorityQueue<>();// O(NlogK)

        for (int i = 0; i < len; i++)
            workers[i] = new double[]{(double)(wage[i]) / quality[i], (double)quality[i]};
        Arrays.sort(workers, (a, b) -> Double.compare(a[0], b[0]));// O(NlogN) 按cp值由小到大排序

        for (double[] worker: workers) {
            qsum += worker[1];
            pq.offer(-worker[1]);
            if (pq.size() > k) qsum += pq.poll();// 將堆頂能力值最大的员工移除，因為能力值越大意味需要付的薪水越多
            if (pq.size() == k) res = Math.min(res, qsum * worker[0]);// 最少金額會等於 最差cp值* 總q
        }
        /**
        quality =
            [5,10,20]
	        wage =
            [5,10,30]
        */
        return res;
        
    }
}
```

![Untitled](Untitled%201.png)