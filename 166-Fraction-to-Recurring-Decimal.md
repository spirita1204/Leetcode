# 166. Fraction to Recurring Decimal

Methods: Basic logic, Math
Difficulty: Medium

Medium

Topics

Companies

Hint

Given two integers representing the `numerator` and `denominator` of a fraction, return *the fraction in string format*.

If the fractional part is repeating, enclose the repeating part in parentheses.

If multiple answers are possible, return **any of them**.

It is **guaranteed** that the length of the answer string is less than `104` for all the given inputs.

**Example 1:**

```
Input: numerator = 1, denominator = 2
Output: "0.5"

```

**Example 2:**

```
Input: numerator = 2, denominator = 1
Output: "2"

```

**Example 3:**

```
Input: numerator = 4, denominator = 333
Output: "0.(012)"

```

**Constraints:**

- `231 <= numerator, denominator <= 231 - 1`
- `denominator != 0`

```java
class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        // 做長除法規律 -> r開始重複-> 代表repeat()
        StringBuilder sb = new StringBuilder();
        if (numerator == 0) return "0";
        // "+" or "-"
        sb.append(((numerator > 0) ^ (denominator > 0)) ? "-" : "");
        // 都轉正數處理, 可能有溢位情況(除法每次補0) 所以用long
        long num = Math.abs((long)numerator);
        long den = Math.abs((long)denominator);
        // 整數位
        if(num >= den) sb.append(num / den);
        else sb.append(0);
        // 小數點
        if(num % den != 0) sb.append(".");
        num %= den;
        // 小數點後 4/9=0.444, 4/333=0.012012
        StringBuilder sb1 = new StringBuilder();
        Map<Long, Integer> hm = new HashMap<>();
        hm.put(num, sb.length());
        while(num != 0) {
            num *= 10;
            sb.append(num/ den);
            num %= den;
            if(hm.containsKey(num)) {// 確認是否包含 有的話 找出重複的 開始座標
                int index = hm.get(num);
                sb.insert(index, "(");
                sb.append(")");
                break;
            } else {// sb.length() 即為index 
                hm.put(num, sb.length());
            }
        }
        return sb.toString();
    }
}
```