# 402. Remove K Digits

Data structure: Stack
Difficulty: Medium

Medium

Topics

Companies

Given string num representing a non-negative integer `num`, and an integer `k`, return *the smallest possible integer after removing* `k` *digits from* `num`.

**Example 1:**

```
Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.

```

**Example 2:**

```
Input: num = "10200", k = 1
Output: "200"
Explanation: Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.

```

**Example 3:**

```
Input: num = "10", k = 2
Output: "0"
Explanation: Remove all the digits from the number and it is left with nothing which is 0.

```

**Constraints:**

- `1 <= k <= num.length <= 105`
- `num` consists of only digits.
- `num` does not have any leading zeros except for the zero itself.

```java
class Solution {
    public String removeKdigits(String num, int k) {
        if (k == num.length()) return "0";// 當刪除數量等同字串長度
        Stack<Character> stack = new Stack<>();
        int i = 0;
        while (i < num.length()) {
            // whenever meet a digit which is less than the previous digit, discard the
            // previous one
            while (k > 0 && !stack.isEmpty() && stack.peek() > num.charAt(i)) {
                stack.pop();
                k--;
            }
            stack.push(num.charAt(i));
            i++;
        }
        while(k-- > 0) stack.pop();// 當都為升序 k無刪除

        StringBuilder sb = new StringBuilder();
        while (!stack.isEmpty()) {
            System.out.println(stack.peek() + "aa");
            sb.append(stack.pop());
        }
        sb.reverse();
        String res = sb.toString().replaceFirst("^0*", "");

        return ("".equals(res)) ? "0" : res;
    }
}
```