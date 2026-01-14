# 3003. Maximize the Number of Partitions After Operations  

  Methods: Bitwise </br> Difficulty: Hard </br> </br>You are given a string `s` and an integer `k`.

First, you are allowed to change **at most** **one** index in `s` to another lowercase English letter.

After that, do the following partitioning operation until `s` is **empty**:

- Choose the **longest** **prefix** of `s` containing at most `k` **distinct** characters.
- **Delete** the prefix from `s` and increase the number of partitions by one. The remaining characters (if any) in `s` maintain their initial order.
Return an integer denoting the **maximum** number of resulting partitions after the operations by optimally choosing at most one index to change.

**Example 1:**

**Input:** s = "accca", k = 2

**Output:** 3

**Explanation:**

The optimal way is to change `s[2]` to something other than a and c, for example, b. then it becomes `"acbca"`.

Then we perform the operations:

1. The longest prefix containing at most 2 distinct characters is `"ac"`, we remove it and `s` becomes `"bca"`.
1. Now The longest prefix containing at most 2 distinct characters is `"bc"`, so we remove it and `s` becomes `"a"`.
1. Finally, we remove `"a"` and `s` becomes empty, so the procedure ends.
Doing the operations, the string is divided into 3 partitions, so the answer is 3.

**Example 2:**

**Input:** s = "aabaab", k = 3

**Output:** 1

**Explanation:    **

Initially `s` contains 2 distinct characters, so whichever character we change, it will contain at most 3 distinct characters, so the longest prefix with at most 3 distinct characters would always be all of it, therefore the answer is 1.

**Example 3:   **

**Input:** s = "xxyz", k = 1    

**Output:** 4

**Explanation:**

The optimal way is to change `s[0]` or `s[1]` to something other than characters in `s`, for example, to change `s[0]` to `w`.

Then `s` becomes `"wxyz"`, which consists of 4 distinct characters, so as `k` is 1, it will divide into 4 partitions.

**Constraints:     **

- `1 <= s.length <= 104`
- `s` consists only of lowercase English letters.
- `1 <= k <= 26`   
```java
class Solution {
    public int maxPartitionsAfterOperations(String s, int k) {
        if (k == 26) return 1;
        
        int n = s.length();
        int[] leftMask = new int[n];
        int[] leftDup = new int[n];
        int[] leftParts = new int[n];
        // 不改字時切有多少parts(左掃)
        int mask = 0;// 目前這一段有哪些字
        int dup = 0;// 有沒有「重複字元」
        int parts = 1;// 到目前為止切了幾段
        for (int i = 0; i < n; i++) {
            int bit = 1 << (s.charAt(i) - 'a');
            dup |= mask & bit;// bit 已經在 mask 裡 表示重複
            mask |= bit;
            if (Integer.bitCount(mask) > k) {
                mask = bit;
                dup = 0;
                parts++;
            }
            leftMask[i] = mask;// i 所在段的字元集合
            leftDup[i] = dup;// i 所在段是否有重複字
            leftParts[i] = parts;// 從左到 i 會切幾段
        }
        // 從「右邊」再掃一次(改字發生在 i 右邊會怎麼被切)
        int result = parts;
        mask = 0;
        dup = 0;
        parts = 0;
        
        for (int i = n - 1; i >= 0; i--) {
            int bit = 1 << (s.charAt(i) - 'a');
            dup |= mask & bit;
            mask |= bit;
            
            int bitCount = Integer.bitCount(mask);
            if (bitCount > k) {// 如果 distinct 超過 k, 就必須「切一段」,新的一段只剩目前這個字母
                mask = bit;
                dup = 0;
                parts++;
            }
            // 右邊這一段已經滿
            if (bitCount == k) {
                if (((bit & dup) != 0) && // 右邊這段有重複字（能替換）
                    ((bit & leftDup[i]) != 0) && // 左邊這段也有重複字
                    (Integer.bitCount(leftMask[i]) == k) && // 左邊 distinct 也是 k
                    ((leftMask[i] | mask) != 0x3FFFFFF)) {// 左右合起來 還有新字可以換
                    result = Math.max(result, parts + leftParts[i] + 2);// 改一個字：左邊爆一次, 右邊也爆一次
                } else if (dup != 0) {// 右邊有重複字 改成新字，右邊會爆
                    result = Math.max(result, parts + leftParts[i] + 1);
                }
            }
        }
        
        return result;
    }
}
```

