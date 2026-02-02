# 3013. Divide an Array Into Subarrays With Minimum Cost II  

  Methods: Sliding Window </br> Data Structure: Hash Table </br> Difficulty: Hard </br> </br>You are given a **0-indexed** array of integers `nums` of length `n`, and two **positive** integers `k` and `dist`.

The **cost** of an array is the value of its **first** element. For example, the cost of `[1,2,3]` is `1` while the cost of `[3,4,1]` is `3`.

You need to divide `nums` into `k` **disjoint contiguous **subarrays, such that the difference between the starting index of the **second** subarray and the starting index of the `kth` subarray should be **less than or equal to** `dist`. In other words, if you divide `nums` into the subarrays `nums[0..(i1 - 1)], nums[i1..(i2 - 1)], ..., nums[ik-1..(n - 1)]`, then `ik-1 - i1 <= dist`.

Return *the ****minimum**** possible sum of the cost of these* *subarrays*.   

**Example 1:  **

```plain text
Input: nums = [1,3,2,6,4,2], k = 3, dist = 3
Output: 5
Explanation: The best possible way to divide nums into 3 subarrays is: [1,3], [2,6,4], and [2]. This choice is valid because ik-1 - i1 is 5 - 2 = 3 which is equal to dist. The total cost is nums[0] + nums[2] + nums[5] which is 1 + 2 + 2 = 5.
It can be shown that there is no possible way to divide nums into 3 subarrays at a cost lower than 5.
```

**Example 2:**

```plain text
Input: nums = [10,1,2,2,2,1], k = 4, dist = 3
Output: 15
Explanation: The best possible way to divide nums into 4 subarrays is: [10], [1], [2], and [2,2,1]. This choice is valid because ik-1 - i1 is 3 - 1 = 2 which is less than dist. The total cost is nums[0] + nums[1] + nums[2] + nums[3] which is 10 + 1 + 2 + 2 = 15.
The division [10], [1], [2,2,2], and [1] is not valid, because the difference between ik-1 and i1 is 5 - 1 = 4, which is greater than dist.
It can be shown that there is no possible way to divide nums into 4 subarrays at a cost lower than 15.
```

**Example 3:**

```plain text
Input: nums = [10,8,18,9], k = 3, dist = 1
Output: 36
Explanation: The best possible way to divide nums into 4 subarrays is: [10], [8], and [18,9]. This choice is valid because ik-1 - i1 is 2 - 1 = 1 which is equal to dist.The total cost is nums[0] + nums[1] + nums[2] which is 10 + 8 + 18 = 36.
The division [10], [8,18], and [9] is not valid, because the difference between ik-1 and i1 is 3 - 1 = 2, which is greater than dist.
It can be shown that there is no possible way to divide nums into 3 subarrays at a cost lower than 36.
```

**Constraints:**

- `3 <= n <= 105`
- `1 <= nums[i] <= 109`
- `3 <= k <= n`
- `k - 2 <= dist <= n - 2`
```java
class Solution {
    static class SmartWindow {
        int K;
        TreeMap<Integer, Integer> low = new TreeMap<>();// 存最小的 K 個數
        TreeMap<Integer, Integer> high = new TreeMap<>();// 存剩下的
        long sumLow = 0;                                // low 裡所有元素的總和
        int szLow = 0, szHigh = 0;
        SmartWindow(int k){
            this.K = k;
        }
        int windowSize(){
            return szLow + szHigh;
        }
        private void addMap(TreeMap<Integer, Integer> mp, int x){
            mp.put(x, mp.getOrDefault(x, 0) + 1);
        }
        private boolean removeMap(TreeMap<Integer, Integer> mp, int x){
            Integer c = mp.get(x);
            if (c == null) return false;
            if (c == 1) mp.remove(x);
            else mp.put(x, c - 1);
            return true;
        }
        private int popLast(TreeMap<Integer, Integer> mp){
            int x = mp.lastKey();
            removeMap(mp, x);
            return x;
        }
        private int popFirst(TreeMap<Integer, Integer> mp){
            int x = mp.firstKey();
            removeMap(mp, x);
            return x;
        }
        void rebalance(){
            // low 裡的元素數量
            int need = Math.min(K, windowSize());
            // low 放太多了
            while(szLow > need){
                // 把 low 最大的丟到 high
                int x = popLast(low);
                szLow --;
                sumLow -= x;
                addMap(high, x);
                szHigh ++;
            }
            // low 不夠
            while(szLow < need && szHigh > 0){
                // 把 high 最小的補進 low
                int x = popFirst(high);
                szHigh --;
                addMap(low, x);
                szLow ++;
                sumLow += x;
            }
            // low 永遠是 window 中最小的 K 個
        }
        void add(int x){
            // 如果 low 是空的 → 直接丟進 low
            // 否則比較：
            // x <= low 最大值 → 應該屬於「小的那群」
            // 否則 → 放進 high
            // 最後 rebalance()
            if(szLow == 0){
                addMap(low, x);
                szLow ++;
                sumLow += x;
            }
            else{
                int mxLow = low.lastKey();
                if(x <= mxLow){
                    addMap(low, x);
                    szLow ++;
                    sumLow += x;
                }
                else {
                    addMap(high, x);
                    szHigh ++;
                }
            }
            rebalance();
        }
        void remove(int x){
            // 嘗試從 low 移除
            // 不在 low → 從 high 移除
            // 移完後 rebalance()
            if(removeMap(low, x)){
                szLow --;
                sumLow -= x;
            }
            else if(removeMap(high, x)){
                szHigh --;
            }
            rebalance();
        }
        long query(){
            return sumLow;
        }
    }

    public long minimumCost(int[] nums, int k, int dist) {
        int n = nums.length;
        k -= 1;
        SmartWindow window = new SmartWindow(k);
        // 假設[0][1~1+dist][dist+1...]
        for(int i = 1; i <= 1 + dist; i++){// dist
            window.add(nums[i]);// ik-1 ∈ [1, 1+dist]
        }
        long ans = window.query();// k - 1個最小sum
        // 每次：
        // window 往右移一格
        // 保持長度 = dist + 1
        // 算目前 window 中 最小 k−1 個數的總和
        for(int i = 2; i + dist < n; i ++){
            window.remove(nums[i - 1]);
            window.add(nums[i + dist]);
            ans = Math.min(ans, window.query());
        }
        // ans = 最小的 k−1 個起點 cost
        // nums[0] = 第一個 subarray cost（必選）
        return ans + nums[0];
    }
}
```

