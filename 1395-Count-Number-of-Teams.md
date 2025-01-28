# 1395. Count Number of Teams

Methods: DP
Difficulty: Medium

Medium

Topics

Companies

Hint

There are `n` soldiers standing in a line. Each soldier is assigned a **unique** `rating` value.

You have to form a team of 3 soldiers amongst them under the following rules:

- Choose 3 soldiers with index (`i`, `j`, `k`) with rating (`rating[i]`, `rating[j]`, `rating[k]`).
- A team is valid if: (`rating[i] < rating[j] < rating[k]`) or (`rating[i] > rating[j] > rating[k]`) where (`0 <= i < j < k < n`).

Return the number of teams you can form given the conditions. (soldiers can be part of multiple teams).

**Example 1:**

```
Input: rating = [2,5,3,4,1]
Output: 3
Explanation: We can form three teams given the conditions. (2,3,4), (5,4,1), (5,3,1).

```

**Example 2:**

```
Input: rating = [2,1,3]
Output: 0
Explanation: We can't form any team given the conditions.

```

**Example 3:**

```
Input: rating = [1,2,3,4]
Output: 4

```

**Constraints:**

- `n == rating.length`
- `3 <= n <= 1000`
- `1 <= rating[i] <= 105`
- All the integers in `rating` are **unique**.

## 暴力法(n^2)

```java
class Solution {
    public int numTeams(int[] rating) {
        // for every index. sum(leftSmaller*rightBigger+leftbigger*rightSmaller)
        int len = rating.length;
        int res = 0;
        for(int i = 1; i < len - 1; i++) {
            // 找當前索引 左小*右大+ 右大*左小
            int leftMin = 0, rightMax = 0;
            for(int j = 0; j < i; j++) {
                if(rating[j] < rating[i])
                    leftMin++;
            }
            for(int j = i + 1; j < len; j++) {
                if(rating[j] > rating[i])
                    rightMax++;
            }
            res += leftMin* rightMax;
        }
        for(int i = 1; i < len - 1; i++) {
            // 找當前索引 左小*右大+ 右大*左小
            int leftMax = 0, rightMin = 0;
            for(int j = 0; j < i; j++) {
                if(rating[j] > rating[i])
                    leftMax++;
            }
            for(int j = i + 1; j < len; j++) {
                if(rating[j] < rating[i])
                    rightMin++;
            }
            res += leftMax* rightMin;
        }
        return res;
    }
}
```

## DP

```sql
class Solution {
    public int numTeams(int[] rating) {
        int res = 0;
        // DP 
        for (int i = 1; i < rating.length - 1; i++) {// index
            int less[] = new int[2], greater[] = new int[2];
            for (int j = 0; j < rating.length; j++) {// 計算比大小數目
                if (rating[i] < rating[j]) {
                    if(j > i) less[1]++;
                    else less[0]++;
                }
                if (rating[i] > rating[j]) {
                    if(j > i) greater[1]++;
                    else greater[0]++;
                }
            }
            res += less[0] * greater[1] + greater[0] * less[1];
        }
        return res;
    }
}
```