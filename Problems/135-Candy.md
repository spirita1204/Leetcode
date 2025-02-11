# 135. Candy

Methods: Greedy
Difficulty: Hard

Hard

Topics

Companies

There are `n` children standing in a line. Each child is assigned a rating value given in the integer array `ratings`.

You are giving candies to these children subjected to the following requirements:

- Each child must have at least one candy.
- Children with a higher rating get more candies than their neighbors.

Return *the minimum number of candies you need to have to distribute the candies to the children*.

**Example 1:**

```
Input: ratings = [1,0,2]
Output: 5
Explanation: You can allocate to the first, second and third child with 2, 1, 2 candies respectively.

```

**Example 2:**

```
Input: ratings = [1,2,2]
Output: 4
Explanation: You can allocate to the first, second and third child with 1, 2, 1 candies respectively.
The third child gets 1 candy because it satisfies the above two conditions.

```

**Constraints:**

- `n == ratings.length`
- `1 <= n <= 2 * 104`
- `0 <= ratings[i] <= 2 * 104`

```java
class Solution {
    public int candy(int[] ratings) {
        int n = ratings.length;
        int[] res = new int[n];
        Arrays.fill(res, 1);// 每個小朋友先給一顆糖
        int sum = 0;

        for(int i = 1; i < n; i++) {
            // 跟左邊比較是否公平 情境2
            if(ratings[i] > ratings[i - 1]) {
                res[i] = Math.max(1, res[i - 1] + 1);
            }
        }
        for(int i = n - 2; i >= 0; i--) {
            // 跟右邊比較是否公平 情境2
            if(ratings[i] > ratings[i + 1]) {
                res[i] = Math.max(res[i], res[i + 1] + 1);
            }
        }
        for(int i: res) {
            sum += i;
        }
        return sum;
    }
}
```