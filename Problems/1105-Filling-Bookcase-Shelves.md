# 1105. Filling Bookcase Shelves

Methods: DP
Difficulty: Medium, Medium++

Medium

Topics

Companies

Hint

You are given an array `books` where `books[i] = [thicknessi, heighti]` indicates the thickness and height of the `ith` book. You are also given an integer `shelfWidth`.

We want to place these books in order onto bookcase shelves that have a total width `shelfWidth`.

We choose some of the books to place on this shelf such that the sum of their thickness is less than or equal to `shelfWidth`, then build another level of the shelf of the bookcase so that the total height of the bookcase has increased by the maximum height of the books we just put down. We repeat this process until there are no more books to place.

Note that at each step of the above process, the order of the books we place is the same order as the given sequence of books.

- For example, if we have an ordered list of `5` books, we might place the first and second book onto the first shelf, the third book on the second shelf, and the fourth and fifth book on the last shelf.

Return *the minimum possible height that the total bookshelf can be after placing shelves in this manner*.

**Example 1:**

![https://assets.leetcode.com/uploads/2019/06/24/shelves.png](https://assets.leetcode.com/uploads/2019/06/24/shelves.png)

```
Input: books = [[1,1],[2,3],[2,3],[1,1],[1,1],[1,1],[1,2]], shelfWidth = 4
Output: 6
Explanation:
The sum of the heights of the 3 shelves is 1 + 3 + 2 = 6.
Notice that book number 2 does not have to be on the first shelf.

```

**Example 2:**

```
Input: books = [[1,3],[2,4],[3,2]], shelfWidth = 6
Output: 4

```

**Constraints:**

- `1 <= books.length <= 1000`
- `1 <= thicknessi <= shelfWidth <= 1000`
- `1 <= heighti <= 1000`

```java
class Solution {
    public int minHeightShelves(int[][] books, int shelfWidth) {
        // dp[i]: the min height for placing first books i - 1 on shelves
        // sub problem dp[j] => min(dp[j] + max(height[j+1] .. height[i]))
        // where sum(width[j+1] + ... + sum(width[i]) <= shelve_width
        int len = books.length;
        int[] dp = new int[len + 1];
        
        for(int i = 1; i <= len; i++) {
            int width = books[i - 1][0];
            int height = books[i - 1][1];
            // 1.將新書放到新一行
            dp[i] = dp[i - 1] + height;
            // 2.或者將新書和其他書一起拿出來放同一層
            for(int j = i - 1; j > 0; j--) {
                height = Math.max(height, books[j - 1][1]);// 取最高
                if(width + books[j - 1][0] > shelfWidth)// 總長度超過書櫃
                    break;
                width += books[j - 1][0];// 累加寬度
                dp[i] = Math.min(dp[i], dp[j - 1] + height);
            }
        }
        return dp[len];
    }
}
```