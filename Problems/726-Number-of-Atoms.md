# 726. Number of Atoms

Data structure: Hash Table, Stack
Difficulty: Hard

Hard

Topics

Companies

Hint

Given a string `formula` representing a chemical formula, return *the count of each atom*.

The atomic element always starts with an uppercase character, then zero or more lowercase letters, representing the name.

One or more digits representing that element's count may follow if the count is greater than `1`. If the count is `1`, no digits will follow.

- For example, `"H2O"` and `"H2O2"` are possible, but `"H1O2"` is impossible.

Two formulas are concatenated together to produce another formula.

- For example, `"H2O2He3Mg4"` is also a formula.

A formula placed in parentheses, and a count (optionally added) is also a formula.

- For example, `"(H2O2)"` and `"(H2O2)3"` are formulas.

Return the count of all elements as a string in the following form: the first name (in sorted order), followed by its count (if that count is more than `1`), followed by the second name (in sorted order), followed by its count (if that count is more than `1`), and so on.

The test cases are generated so that all the values in the output fit in a **32-bit** integer.

**Example 1:**

```
Input: formula = "H2O"
Output: "H2O"
Explanation: The count of elements are {'H': 2, 'O': 1}.

```

**Example 2:**

```
Input: formula = "Mg(OH)2"
Output: "H2MgO2"
Explanation: The count of elements are {'H': 2, 'Mg': 1, 'O': 2}.

```

**Example 3:**

```
Input: formula = "K4(ON(SO3)2)2"
Output: "K4N2O14S4"
Explanation: The count of elements are {'K': 4, 'N': 2, 'O': 14, 'S': 4}.

```

**Constraints:**

- `1 <= formula.length <= 1000`
- `formula` consists of English letters, digits, `'('`, and `')'`.
- `formula` is always valid.

```java
class Solution {
    public String countOfAtoms(String formula) {
        Stack<Map<String, Integer>> st = new Stack<>();
        Map<String, Integer> hm = new HashMap<>();// 單字 -> 數量
        int i = 0, len = formula.length();
        while (i < len) {
            char c = formula.charAt(i);
            i++;// 到下一位 判斷用
            if (c == '(') {
                st.push(hm);
                hm = new HashMap<>();// 新的group
            } else if (c == ')') {
                int val = 0;
                while (i < len && Character.isDigit(formula.charAt(i)))
                    val = val * 10 + formula.charAt(i++) - '0';
                if (val == 0)
                    val = 1;
                if (!st.isEmpty()) {
                    Map<String, Integer> temp = hm;// 當前集合
                    hm = st.pop();// 外層集合
                    for (String key : temp.keySet())// 處理括號後面數字加總
                        hm.put(key, hm.getOrDefault(key, 0) + temp.get(key) * val);
                }
            } else {// 字母或數字
                int start = i - 1;
                while (i < len && Character.isLowerCase(formula.charAt(i))) {
                    i++;// 同時控制i往後移
                }
                // 取得完整元素
                String s = formula.substring(start, i);
                int val = 0;
                while (i < len && Character.isDigit(formula.charAt(i)))
                    // 可能有多位數字
                    val = val * 10 + formula.charAt(i++) - '0';
                if (val == 0)// 一個元素
                    val = 1;
                hm.put(s, hm.getOrDefault(s, 0) + val);
            }
        }
        StringBuilder sb = new StringBuilder();
        List<String> list = new ArrayList<>(hm.keySet());
        Collections.sort(list);
        for (String key : list) {
            sb.append(key);
            if (hm.get(key) > 1)
                sb.append(hm.get(key));
        }
        return sb.toString();
    }
}
```