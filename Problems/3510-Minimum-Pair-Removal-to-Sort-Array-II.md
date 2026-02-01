# 3510. Minimum Pair Removal to Sort Array II  

  Methods: Greedy </br> Data Structure: Heap </br> Difficulty: Hard </br> </br>Given an array `nums`, you can perform the following operation any number of times:   

- Select the **adjacent** pair with the **minimum** sum in `nums`. If multiple such pairs exist, choose the leftmost one.
- Replace the pair with their sum.  
Return the **minimum number of operations** needed to make the array **non-decreasing**.  

An array is said to be **non-decreasing** if each element is greater than or equal to its previous element (if it exists).

**Example 1:  **

**Input:** nums = [5,2,3,1]

**Output:** 2  

**Explanation:  **

- The pair `(3,1)` has the minimum sum of 4. After replacement, `nums = [5,2,4]`.
- The pair `(2,4)` has the minimum sum of 6. After replacement, `nums = [5,6]`.
The array `nums` became non-decreasing in two operations.

**Example 2:  **

**Input:** nums = [1,2,2]    

**Output:** 0 

**Explanation:  **

The array `nums` is already sorted.  

**Constraints:   **

- `1 <= nums.length <= 105`   
- `109 <= nums[i] <= 109`
```java
class Solution {
    public int minimumPairRemoval(int[] nums) {
        // greedy 
        int n = nums.length;
        if (n == 1)
            return 0;

        long[] arr = new long[n];
        for (int i = 0; i < n; i++)
            arr[i] = nums[i];
        boolean[] removed = new boolean[n];// 紀錄是否被合併

        PriorityQueue<P> pq = new PriorityQueue<>(// 先比 sum（小的優先）一樣再筆idx小的先
                (a, b) -> {
                    if (a.sum < b.sum)  
                        return -1;
                    if (a.sum > b.sum)
                        return 1;
                    return Integer.compare(a.idx, b.idx);
                });

        int sorted = 0;
        for (int i = 1; i < n; i++) {
            pq.offer(new P(arr[i - 1] + arr[i], i - 1));// sum, idx
            if (arr[i] >= arr[i - 1])
                sorted++;
        }
        if (sorted == n - 1)// 本身就是non-decreasing
            return 0;

        int rem = n;
        int[] prev = new int[n];
        int[] next = new int[n];
        for (int i = 0; i < n; i++) {// 紀錄前後關係
            prev[i] = i - 1;
            next[i] = i + 1;
        }

        while (rem > 1) {// 只要還能合併，就繼續
            P top = pq.poll();// greedy
            if (top == null)
                break;
            long sum = top.sum;
            int left = top.idx;
            int right = next[left];
            if (right >= n || removed[left] || removed[right] || arr[left] + arr[right] != sum)
                continue;

            int pre = prev[left];
            int nxt = next[right];// pre->left->right->nxt
            // 更新 sorted（合併前先扣）
            if (arr[left] <= arr[right])
                sorted--;
            if (pre != -1 && arr[pre] <= arr[left])
                sorted--;
            if (nxt != n && arr[right] <= arr[nxt])
                sorted--;
            // 真的合併
            arr[left] += arr[right];
            removed[right] = true;
            rem--;  

            if (pre != -1) {
                pq.offer(new P(arr[pre] + arr[left], pre));
                if (arr[pre] <= arr[left])
                    sorted++;
            } else {
                prev[left] = -1;
            }

            if (nxt != n) {
                prev[nxt] = left;
                next[left] = nxt;
                pq.offer(new P(arr[left] + arr[nxt], left));
                if (arr[left] <= arr[nxt])
                    sorted++;
            } else {
                next[left] = n;
            }
            // 需要核定次數
            if (sorted == rem - 1)
                return n - rem;
        }
        return n;
    }    

    private static class P {
        long sum;
        int idx;

        P(long sum, int idx) {
            this.sum = sum;
            this.idx = idx;
        }
    }   

}     

```



