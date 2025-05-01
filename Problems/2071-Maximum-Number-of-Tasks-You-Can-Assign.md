# 2071. Maximum Number of Tasks You Can Assign  

  Methods: Binary Search,Greedy </br> Data Structure: Queue </br> Difficulty: Hard </br> </br>You have `n` tasks and `m` workers. Each task has a strength requirement stored in a **0-indexed** integer array `tasks`, with the `ith` task requiring `tasks[i]` strength to complete. The strength of each worker is stored in a **0-indexed** integer array `workers`, with the `jth` worker having `workers[j]` strength. Each worker can only be assigned to a **single** task and must have a strength **greater than or equal** to the task's strength requirement (i.e., `workers[j] >= tasks[i]`).

Additionally, you have `pills` magical pills that will **increase a worker's strength** by `strength`. You can decide which workers receive the magical pills, however, you may only give each worker **at most one** magical pill.

Given the **0-indexed **integer arrays `tasks` and `workers` and the integers `pills` and `strength`, return *the ****maximum**** number of tasks that can be completed.*

**Example 1:**

```plain text
Input: tasks = [3,2,1], workers = [0,3,3], pills = 1, strength = 1
Output: 3
Explanation:
We can assign the magical pill and tasks as follows:
- Give the magical pill to worker 0.
- Assign worker 0 to task 2 (0 + 1 >= 1)
- Assign worker 1 to task 1 (3 >= 2)
- Assign worker 2 to task 0 (3 >= 3)

```

**Example 2:**

```plain text
Input: tasks = [5,4], workers = [0,0,0], pills = 1, strength = 5
Output: 1
Explanation:
We can assign the magical pill and tasks as follows:
- Give the magical pill to worker 0.
- Assign worker 0 to task 0 (0 + 5 >= 5)

```

**Example 3:**

```plain text
Input: tasks = [10,15,30], workers = [0,10,10,10,10], pills = 3, strength = 10
Output: 2
Explanation:
We can assign the magical pills and tasks as follows:
- Give the magical pill to worker 0 and worker 1.
- Assign worker 0 to task 0 (0 + 10 >= 10)
- Assign worker 1 to task 1 (10 + 10 >= 15)
The last pill is not given because it will not make any worker strong enough for the last task.

```

**Constraints:**

- `n == tasks.length`
- `m == workers.length`
- `1 <= n, m <= 5 * 104`
- `0 <= pills <= m`
- `0 <= tasks[i], workers[j], strength <= 109`
```java
class Solution {
    public int maxTaskAssign(int[] tasks, int[] workers, int pills, int strength) {
        // greedy
        Arrays.sort(tasks);
        Arrays.sort(workers);
    
        int n = tasks.length;
        int m = workers.length;
        // BS
        int left = 0, right = Math.min(m, n);
        
        while (left < right) {
            int mid = (left + right + 1) / 2;
            if (check(mid, tasks, workers, pills, strength, n, m)) {
                left = mid;
            } else {
                right = mid - 1;
            }
        }
        return left;
    }

    /**
        是否能夠完成 x 個任務

        @param x 中位數
        @param tasks
        @param workers
        @param pills
        @param strength
        @param n 任務數量
        @param m 勞工數量
    */
    private boolean check(int x, int[] tasks, int[] workers, int pills, int strength, int n, int m) {
        int i = 0;
        Deque<Integer> q = new ArrayDeque<>();// 能夠由工人完成的任務存

        for (int j = m - x; j < m; j++) {
            while (i < x && tasks[i] <= workers[j] + strength) {
                q.offer(tasks[i]);
                i++;
            }
            if (q.isEmpty()) // 沒有任務能完成
                return false;
            
            if (q.peekFirst() <= workers[j]) {// 不用吃藥
                q.pollFirst();
            } else if (pills == 0) {// 剛好沒藥
                return false;
            } else {// 要吃藥並去做要求力量最大的任務
                --pills;
                q.pollLast();
            }
        }
        return true;
    }
}
```

