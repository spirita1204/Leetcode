# 3272. Find the Count of Good Integers  

  Methods: Combinatorics </br> Difficulty: Hard </br> </br>You are given two **positive** integers `n` and `k`.

An integer `x` is called **k-palindromic** if:

- `x` is a .
- `x` is divisible by `k`.
An integer is called **good** if its digits can be *rearranged* to form a **k-palindromic** integer. For example, for `k = 2`, 2020 can be rearranged to form the *k-palindromic* integer 2002, whereas 1010 cannot be rearranged to form a *k-palindromic* integer.

Return the count of **good** integers containing `n` digits.

**Note** that *any* integer must **not** have leading zeros, **neither** before **nor** after rearrangement. For example, 1010 *cannot* be rearranged to form 101.

---

**Example 1:**

**Input:** n = 3, k = 5

**Output:** 27

**Explanation:**

*Some* of the good integers are:

- 551 because it can be rearranged to form 515.
- 525 because it is already k-palindromic.
---

**Example 2:**

**Input:** n = 1, k = 4

**Output:** 2

**Explanation:**

The two good integers are 4 and 8.

---

**Example 3:**

**Input:** n = 5, k = 6

**Output:** 2468

---

**Constraints:**

- `1 <= n <= 10`
- `1 <= k <= 9`
```java
class Solution {
    public long countGoodIntegers(int n, int k) {
        long[] fac = new long[n + 1];  // 計算階乘
        fac[0] = 1;
        for (int i = 1; i <= n; i++) 
            fac[i] = fac[i - 1] * i;  // 填充階乘
        
        long ans = 0;
        Set<String> vis = new HashSet<>();  
        int base = (int) Math.pow(10, (n - 1) / 2);  // 回文數的範圍

        // 從base到base*10之間的數字會生成回文數
        for (int i = base; i < base * 10; i++) {
            String s = String.valueOf(i); 
            StringBuilder sb = new StringBuilder(s).reverse();  
            s += sb.substring(n % 2);  // 如果是奇數長度，刪去反轉的中樞數字
            
            if (Long.parseLong(s) % k != 0) 
                continue;  // 如果不是k的倍數，跳過
            
            char[] arr = s.toCharArray();  
            Arrays.sort(arr); 
            String t = new String(arr); 
            
            if (vis.contains(t)) 
                continue;
            vis.add(t);  

            int[] cnt = new int[10];  // 每個數字的頻次
            for (char c : arr) 
                cnt[c - '0']++;

            long res = (n - cnt[0]) * fac[n - 1];  // 計算有效的排列數
            for (int x : cnt) 
                res /= fac[x];  // 重複數字

            ans += res; 
        }

        return ans;
    }
}

```

