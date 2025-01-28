# 670. Maximum Swap

Methods: Greedy
Difficulty: Medium

Medium

Topics

Companies

You are given an integer `num`. You can swap two digits at most once to get the maximum valued number.

Return *the maximum valued number you can get*.

**Example 1:**

```
Input: num = 2736
Output: 7236
Explanation: Swap the number 2 and the number 7.

```

**Example 2:**

```
Input: num = 9973
Output: 9973
Explanation: No swap.

```

**Constraints:**

- `0 <= num <= 108`

```java
class Solution {
    public int maximumSwap(int num) {
        // 7632 先找出最大數
        // 2736 再從左到右開始比
        // 9937 輸出第一個不一樣
        // 9973
        int digit = (int) (Math.log10(num)) + 1;// 幾位
        int[] digits = new int[digit];
        int i = 0;
        while (num > 0) {
            digits[i++] = num % 10;
            num /= 10;
        }
        int[] arrOri = Arrays.copyOf(digits, digit);
        Arrays.sort(digits);
        int p1 = 0, p2 = 0;
        for (int idx = digit - 1; idx >= 0; idx--) {
            if (arrOri[idx] != digits[idx]) {
                p1 = arrOri[idx];
                p2 = digits[idx];
                break;
            }
        }
        int left = 0, right = digit - 1;
        while (arrOri[left] != p2 || arrOri[right] != p1) {
            // 不用交換
            if(left >= right) break;
            if (arrOri[left] != p2)
                left++;
            if (arrOri[right] != p1)
                right--;
        }
        if(left < right) {
            int tmp = arrOri[left];
            arrOri[left] = arrOri[right];
            arrOri[right] = tmp;
        }
        int ten = 1;
        int res = 0;
        for (int a : arrOri) {
            res += a * ten;
            ten *= 10;
        }
        return res;
    }
}
```