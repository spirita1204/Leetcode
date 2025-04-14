# 1534. Count Good Triplets  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>Given an array of integers `arr`, and three integers `a`, `b` and `c`. You need to find the number of good triplets.

A triplet `(arr[i], arr[j], arr[k])` is **good** if the following conditions are true:

- `0 <= i < j < k < arr.length`
- `|arr[i] - arr[j]| <= a`
- `|arr[j] - arr[k]| <= b`
- `|arr[i] - arr[k]| <= c`
Where `|x|` denotes the absolute value of `x`.

Return* the number of good triplets*.

**Example 1:**

```plain text
Input: arr = [3,0,1,1,9,7], a = 7, b = 2, c = 3
Output: 4
Explanation: There are 4 good triplets: [(3,0,1), (3,0,1), (3,1,1), (0,1,1)].
```

**Example 2:**

```plain text
Input: arr = [1,1,2,2,3], a = 0, b = 0, c = 1
Output: 0
Explanation:No triplet satisfies all conditions.
```

**Constraints:**

- `3 <= arr.length <= 100`
- `0 <= arr[i] <= 1000`
- `0 <= a, b, c <= 1000`
```java
class Solution {
    public int countGoodTriplets(int[] arr, int a, int b, int c) {
        int res = 0;
        int len = arr.length;

        for(int i = 0; i < len; i++) {
            for(int j = i + 1; j < len; j++) {
                for(int k = j + 1; k < len; k++) {
                    if(Math.abs(arr[j] - arr[i]) <= a 
                        && Math.abs(arr[k] - arr[j]) <= b
                            && Math.abs(arr[k] - arr[i]) <= c) 
                        res++;
                }
            }
        }
        return res;
    }
}
```

最優解

```java
class Solution {
    public int countGoodTriplets(int[] arr, int a, int b, int c) {
        int ans = 0, n = arr.length;
        int[] sum = new int[1001];
        for (int j = 0; j < n; ++j) {
            for (int k = j + 1; k < n; ++k) {
                if (Math.abs(arr[j] - arr[k]) <= b) {
                    int lj = arr[j] - a, rj = arr[j] + a;
                    int lk = arr[k] - c, rk = arr[k] + c;
                    int l = Math.max(0, Math.max(lj, lk));
                    int r = Math.min(1000, Math.min(rj, rk));
                    if (l <= r) {
                        if (l == 0) {
                            ans += sum[r];// count values <= r
                        } else {
                            ans += sum[r] - sum[l - 1];// Count values between l and r
                        }
                    }
                }
            }
            for (int k = arr[j]; k <= 1000; ++k) {
                ++sum[k];
            }
        }
        return ans;
    }
}
```

