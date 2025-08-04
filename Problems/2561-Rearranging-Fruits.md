# 2561. Rearranging Fruits  

  Methods: Greedy </br> Data Structure: Hash Table </br> Difficulty: Hard </br> </br>You have two fruit baskets containing `n` fruits each. You are given two **0-indexed** integer arrays `basket1` and `basket2` representing the cost of fruit in each basket. You want to make both baskets **equal**. To do so, you can use the following operation as many times as you want:

- Choose two indices `i` and `j`, and swap the `ith` fruit of `basket1` with the `jth` fruit of `basket2`.  
- The cost of the swap is `min(basket1[i], basket2[j])`.
Two baskets are considered equal if sorting them according to the fruit cost makes them exactly the same baskets.  

Return *the minimum cost to make both the baskets equal or *`-1`* if impossible.*

**Example 1:**

```plain text
Input: basket1 = [4,2,2,2], basket2 = [1,4,1,2]
Output: 1
Explanation: Swap index 1 of basket1 with index 0 of basket2, which has cost 1. Now basket1 = [4,1,2,2] and basket2 = [2,4,1,2]. Rearranging both the arrays makes them equal.
```

**Example 2:**

```plain text
Input: basket1 = [2,3,4,1], basket2 = [3,2,5,1]
Output: -1
Explanation: It can be shown that it is impossible to make both the baskets equal.
```

**Constraints:**

- `basket1.length == basket2.length`
- `1 <= basket1.length <= 105`
- `1 <= basket1[i], basket2[i] <= 109`
```java
class Solution {
    public long minCost(int[] basket1, int[] basket2) {
        Map<Integer, Integer> totalCounts = new HashMap<>();
        for (int fruit : basket1)
            totalCounts.put(fruit, totalCounts.getOrDefault(fruit, 0) + 1);
        for (int fruit : basket2)
            totalCounts.put(fruit, totalCounts.getOrDefault(fruit, 0) + 1);

        long minVal = Long.MAX_VALUE;
        for (Map.Entry<Integer, Integer> entry : totalCounts.entrySet()) {
            if (entry.getValue() % 2 != 0)
                return -1;
            minVal = Math.min(minVal, entry.getKey());
        }

        List<Long> fruitsToSwap = new ArrayList<>();
        Map<Integer, Integer> count1 = new HashMap<>();
        for (int fruit : basket1)
            count1.put(fruit, count1.getOrDefault(fruit, 0) + 1);

        for (Map.Entry<Integer, Integer> entry : totalCounts.entrySet()) {
            int fruit = entry.getKey();
            int diff = count1.getOrDefault(fruit, 0) - (entry.getValue() / 2);
            for (int i = 0; i < Math.abs(diff); i++) {
                fruitsToSwap.add((long) fruit);// 總需要交換的
            }
        }

        Collections.sort(fruitsToSwap);

        long totalCost = 0;
        int swapsToMake = fruitsToSwap.size() / 2;
        for (int i = 0; i < swapsToMake; i++) {
            // 更便宜的替代方案
            // 1.先用 basket1 的 100 跟 basket2 的 1 換（花 1）。
            // 2.現在 basket2 多了一個 100，basket1 多了一個 1。
            // 3.再用 basket1 的 1 跟 basket2 的 90 換（花 1）。
            totalCost += Math.min(fruitsToSwap.get(i), 2 * minVal);
            // totalCost += fruitsToSwap.get(i); (x)
        }

        return totalCost;
    }
}
```

