# 2818. Apply Operations to Maximize Score  

  Methods: Greedy,Math </br> Data Structure: Heap,Stack </br> Difficulty: Hard </br> </br>You are given an array `nums` of `n` positive integers and an integer `k`.

Initially, you start with a score of `1`. You have to maximize your score by applying the following operation at most `k` times:

- Choose any **non-empty** subarray `nums[l, ..., r]` that you haven't chosen previously.
- Choose an element `x` of `nums[l, ..., r]` with the highest **prime score**. If multiple such elements exist, choose the one with the smallest index.
- Multiply your score by `x`.
Here, `nums[l, ..., r]` denotes the subarray of `nums` starting at index `l` and ending at the index `r`, both ends being inclusive.

The **prime score** of an integer `x` is equal to the number of distinct prime factors of `x`. For example, the prime score of `300` is `3` since `300 = 2 * 2 * 3 * 5 * 5`.

Return *the ****maximum possible score**** after applying at most *`k`* operations*.

Since the answer may be large, return it modulo `109 + 7`.

**Example 1:**

```plain text
Input: nums = [8,3,9,3,8], k = 2
Output: 81
Explanation: To get a score of 81, we can apply the following operations:
- Choose subarray nums[2, ..., 2]. nums[2] is the only element in this subarray. Hence, we multiply the score by nums[2]. The score becomes 1 * 9 = 9.
- Choose subarray nums[2, ..., 3]. Both nums[2] and nums[3] have a prime score of 1, but nums[2] has the smaller index. Hence, we multiply the score by nums[2]. The score becomes 9 * 9 = 81.
It can be proven that 81 is the highest score one can obtain.
```

**Example 2:**

```plain text
Input: nums = [19,12,14,6,10,18], k = 3
Output: 4788
Explanation: To get a score of 4788, we can apply the following operations:
- Choose subarray nums[0, ..., 0]. nums[0] is the only element in this subarray. Hence, we multiply the score by nums[0]. The score becomes 1 * 19 = 19.
- Choose subarray nums[5, ..., 5]. nums[5] is the only element in this subarray. Hence, we multiply the score by nums[5]. The score becomes 19 * 18 = 342.
- Choose subarray nums[2, ..., 3]. Both nums[2] and nums[3] have a prime score of 2, but nums[2] has the smaller index. Hence, we multipy the score by nums[2]. The score becomes 342 * 14 = 4788.
It can be proven that 4788 is the highest score one can obtain.
```

**Constraints:**

- `1 <= nums.length == n <= 105`
- `1 <= nums[i] <= 105`
- `1 <= k <= min(n * (n + 1) / 2, 109)`
```java
class Solution {

    final int MOD = 1000000007;  // 取模常數，防止結果溢出

    public int maximumScore(List<Integer> nums, int k) {
        int n = nums.size();  // 取得數組的大小
        List<Integer> primeScores = new ArrayList<>(Collections.nCopies(n, 0));  // 用來存放每個數字的質因數數量

        // 計算每個數字的「質因數數量」
        for (int index = 0; index < n; index++) {
            int num = nums.get(index);

            // 尋找 num 的質因數，從 2 到 sqrt(num)
            for (int factor = 2; factor <= Math.sqrt(num); factor++) {
                if (num % factor == 0) {
                    // 如果能被整除，增加質因數數量
                    primeScores.set(index, primeScores.get(index) + 1);

                    // 移除所有 `factor` 的倍數
                    while (num % factor == 0) num /= factor;
                }
            }

            // 如果 num 仍然大於或等於 2，那麼它本身是質數
            if (num >= 2) primeScores.set(index, primeScores.get(index) + 1);
        }

        // 初始化支配元素的索引：nextDominant（下一個質因數數量更大的元素）和 prevDominant（前一個質因數數量更大的元素）
        int[] nextDominant = new int[n];
        int[] prevDominant = new int[n];
        Arrays.fill(nextDominant, n);  // 默認 nextDominant 為 n（表示沒有更大的元素）
        Arrays.fill(prevDominant, -1);  // 默認 prevDominant 為 -1（表示沒有更小的元素）

        // 單調遞減棧，計算每個元素的前一個和下一個支配元素
        Stack<Integer> decreasingPrimeScoreStack = new Stack<>();
        for (int index = 0; index < n; index++) {
            // 如果當前元素的質因數數量大於棧頂元素的質因數數量，則更新 nextDominant
            while (!decreasingPrimeScoreStack.isEmpty() && primeScores.get(decreasingPrimeScoreStack.peek()) < primeScores.get(index)) {
                int topIndex = decreasingPrimeScoreStack.pop();
                nextDominant[topIndex] = index;  // 更新該元素的下一個支配元素
            }

            // 如果棧不為空，則更新當前元素的前一個支配元素
            if (!decreasingPrimeScoreStack.isEmpty()) prevDominant[index] = decreasingPrimeScoreStack.peek();

            // 將當前索引推入棧中
            decreasingPrimeScoreStack.push(index);
        }

        // 計算每個元素可以作為最大元素出現的子陣列數量
        long[] numOfSubarrays = new long[n];
        for (int index = 0; index < n; index++) {
            numOfSubarrays[index] = ((long) nextDominant[index] - index) * (index - prevDominant[index]);
        }

        // 使用最大堆（PriorityQueue）來按數值大小排序，確保最大值先處理
        Queue<int[]> processingQueue = new PriorityQueue<>((a, b) -> {
            if (b[0] == a[0]) {
                return Integer.compare(a[1], b[1]);  // 若數值相同，按索引升序排序
            }
            return Integer.compare(b[0], a[0]);  // 按數值降序排序
        });

        // 將每個數字和它的索引放入優先隊列
        for (int index = 0; index < n; index++) {
            processingQueue.offer(new int[] { nums.get(index), index });
        }

        long score = 1;  // 初始分數設為 1

        // 當還有操作次數 k 時，繼續選擇數字進行最大化
        while (k > 0) {
            // 從優先隊列中取出數值最大的元素
            int[] top = processingQueue.poll();
            int num = top[0];
            int index = top[1];

            // 計算可以應用的操作次數，為 k 和 num 的子陣列數量中的較小值
            long operations = Math.min((long) k, numOfSubarrays[index]);

            // 更新分數，並將數字的操作次數次冪乘到分數上
            score = (score * power(num, operations)) % MOD;

            // 減少剩餘的操作次數
            k -= operations;
        }

        // 返回最終結果
        return (int) score;
    }

    // 用於計算數字的冪次，並取模 MOD
    private long power(long base, long exponent) {
        long res = 1;

        // 使用二分冪方法計算 base^exponent
        while (exponent > 0) {
            // 當指數為奇數時，乘上基數
            if (exponent % 2 == 1) {
                res = (res * base) % MOD;
            }

            // 指數每次減半，基數每次平方
            base = (base * base) % MOD;
            exponent /= 2;
        }

        return res;
    }
}

```

