# 168. Excel Sheet Column Title

Methods: Basic logic
Difficulty: Easy

Easy

Topics

Companies

Given an integer `columnNumber`, return *its corresponding column title as it appears in an Excel sheet*.

For example:

```
A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28
...

```

**Example 1:**

```
Input: columnNumber = 1
Output: "A"

```

**Example 2:**

```
Input: columnNumber = 28
Output: "AB"

```

**Example 3:**

```
Input: columnNumber = 701
Output: "ZY"

```

**Constraints:**

- `1 <= columnNumber <= 231 - 1`

```java
class Solution {
    public String convertToTitle(int columnNumber) {
        StringBuilder sb = new StringBuilder();

        while(columnNumber > 0) {
            sb.append((char)('A' + (--columnNumber % 26)));
            columnNumber /= 26;
        }
        return sb.reverse().toString();
    }
}
```

更簡潔 但使用recursion 速度較慢 記憶體較多

```java
class Solution {
    public String convertToTitle(int columnNumber) {
        return columnNumber == 0 
            ? "" 
            : convertToTitle(--columnNumber / 26) + (char)('A' + (columnNumber % 26));
    }
}
```