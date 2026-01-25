# 3445. Maximum Difference Between Even and Odd Frequency II  

  Methods: Math,Sliding Window,Bitwise </br> Difficulty: Hard </br> </br>You are given a string `s` and an integer `k`. Your task is to find the **maximum** difference between the frequency of **two** characters, `freq[a] - freq[b]`, in a substring `subs` of `s`, such that:   

- `subs` has a size of **at least** `k`.   
- Character `a` has an *odd frequency* in `subs`.
- Character `b` has a **non-zero** *even frequency* in `subs`.
Return the **maximum** difference.

**Note** that `subs` can contain more than 2 **distinct** characters.

**Example 1:**

**Input:** s = "12233", k = 4

**Output:** -1

**Explanation:**

For the substring `"12233"`, the frequency of `'1'` is 1 and the frequency of `'3'` is 2. The difference is `1 - 2 = -1`.

**Example 2:**

**Input:** s = "1122211", k = 3

**Output:** 1

**Explanation:**

For the substring `"11222"`, the frequency of `'2'` is 3 and the frequency of `'1'` is 2. The difference is `3 - 2 = 1`.

**Example 3:**

**Input:** s = "110", k = 3

**Output:** -1

**Constraints:**

- `3 <= s.length <= 3 * 104`
- `s` consists only of digits `'0'` to `'4'`.
- The input is generated that at least one substring has a character with an even frequency and a character with an odd frequency.
- `1 <= k <= s.length`
```java
class Solution {
    public int maxDifference(String s, int k) {
        int n = s.length();
        int ans = Integer.MIN_VALUE;
        // 最大化 (cnt_a[right] - cnt_b[right]) - (cnt_a[left] - cnt_b[left])   
        // prefix[right] - prefix[left]
        for (char a = '0'; a <= '4'; a++) {
            for (char b = '0'; b <= '4'; b++) {
                // (a, b) 組合只有 20 組
                if (a == b) continue;
                
                int[] best = new int[4];// 在某個 left 奇偶狀態下，最小的 (prev_a - prev_b)
                Arrays.fill(best, Integer.MAX_VALUE);
                int cnt_a = 0, cnt_b = 0;// [0..right] 前綴 a / b 次數
                int prev_a = 0, prev_b = 0;// [0..left] 前綴 a / b 次數
                int left = -1;

                for (int right = 0; right < n; right++) {
                    cnt_a += (s.charAt(right) == a) ? 1 : 0;
                    cnt_b += (s.charAt(right) == b) ? 1 : 0;
                    // 目前 (left+1 .. right) 是合法的 substring(substring 中 b 出現 ≥ 2 次)
                    while (right - left >= k && cnt_b - prev_b >= 2) {
                        int left_status = getStatus(prev_a, prev_b);
                        // 對於這個奇偶狀態的 left 目前看到的最小 (prev_a - prev_b) 是多少？
                        best[left_status] = Math.min(
                                best[left_status],
                                prev_a - prev_b
                        );
                        left++;
                        prev_a += (s.charAt(left) == a) ? 1 : 0;
                        prev_b += (s.charAt(left) == b) ? 1 : 0;
                    }
                    int right_status = getStatus(cnt_a, cnt_b);
                    // 找一個 left，使得 (left+1 .. right) 這段 substring 中
                    // 👉 a 的出現次數是奇數
                    // 👉 b 的出現次數是偶數」
                    int required_status = right_status ^ 0b10;// b xor找相配基偶
                    // 如果曾經存在一個合法的 left，而且它的奇偶狀態能讓 substring 符合條件
                    // → 就用它來更新最大差值
                    if (best[required_status] != Integer.MAX_VALUE) {
                        ans = Math.max(
                                ans,
                                cnt_a - cnt_b - best[required_status]
                        );
                    }
                }
            }
        }
        return ans;
    }
    // 只在乎奇偶，不在乎實際數量
    // cnt_a 奇偶	cnt_b 奇偶	status (binary)	十進位
    // even	even	00	        0
    // even	odd	    01	        1
    // odd	even	10	        2
    // odd	odd	    11	        3
    private int getStatus(int cnt_a, int cnt_b) {
        return ((cnt_a & 1) << 1) | (cnt_b & 1);
    }
}
```

