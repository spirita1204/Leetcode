# 3721. Longest Balanced Subarray II  

  Data Structure: Binary Indexed Tree(Fenwick Tree) </br> Difficulty: Hard </br> </br>[https://www.youtube.com/watch?v=rYBtViWXYeI](https://www.youtube.com/watch?v=rYBtViWXYeI)

You are given an integer array `nums`.   

A **subarray** is called **balanced** if the number of **distinct even** numbers in the subarray is equal to the number of **distinct odd** numbers.

Return the length of the **longest** balanced subarray.

**Example 1:**

**Input:** nums = [2,5,4,3]

**Output:** 4

**Explanation:**

- The longest balanced subarray is `[2, 5, 4, 3]`.
- It has 2 distinct even numbers `[2, 4]` and 2 distinct odd numbers `[5, 3]`. Thus, the answer is 4.
**Example 2:**

**Input:** nums = [3,2,2,5,4]

**Output:** 5

**Explanation:**

- The longest balanced subarray is `[3, 2, 2, 5, 4]`.
- It has 2 distinct even numbers `[2, 4]` and 2 distinct odd numbers `[3, 5]`. Thus, the answer is 5.
**Example 3:**

**Input:** nums = [1,2,3,2]

**Output:** 3

**Explanation:**

- The longest balanced subarray is `[2, 3, 2]`.
- It has 1 distinct even number `[2]` and 1 distinct odd number `[3]`. Thus, the answer is 3.
**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 105`    
```java
class SegmentTree {
    int n;
    int[] minTree, maxTree, lazy;// 暫時沒往下更新的區間加值

    public SegmentTree(int n) {
        this.n = n;
        minTree = new int[4 * n];// 最小 state 值
        maxTree = new int[4 * n];// 最大 state 值
        lazy = new int[4 * n];// lazy propagation（延遲更新）
    }

    private void push(int node, int start, int end) {
        if (lazy[node] != 0) {
            minTree[node] += lazy[node];
            maxTree[node] += lazy[node];
            if (start != end) {// 如果不是葉節點 把這個 lazy 傳給左右子節點。
                lazy[2 * node] += lazy[node];
                lazy[2 * node + 1] += lazy[node];
            }
            lazy[node] = 0;
        }
    }
    // 把區間 [l, r] 全部加上 val
    public void updateRange(int node, int start, int end, int l, int r, int val) {
        push(node, start, end);
        // 區間完全不重疊
        if (start > end || start > r || end < l) {
            return;
        }  
        // 完全覆蓋，這整段都要加 val
        if (l <= start && end <= r) { 
            lazy[node] += val;
            push(node, start, end);
            return;
        }
        int mid = (start + end) / 2;
        // 部分重疊 → 往下遞迴
        updateRange(2 * node, start, mid, l, r, val);
        updateRange(2 * node + 1, mid + 1, end, l, r, val);
        minTree[node] = Math.min(minTree[2 * node], minTree[2 * node + 1]);
        maxTree[node] = Math.max(maxTree[2 * node], maxTree[2 * node + 1]);
    }
    // 找最小的 index i 使 state[i] == 0
    public int findLeftmostZero(int node, int start, int end) {
        push(node, start, end);
        // 這整段裡不可能有 state == 0
        if (minTree[node] > 0 || maxTree[node] < 0) {
            return -1;
        }
        // 葉節點
        if (start == end) {// state == 0
            return minTree[node] == 0 ? start : -1;
        }
        int mid = (start + end) / 2;
        int left = findLeftmostZero(2 * node, start, mid);
        if (left != -1) return left;
        // right
        return findLeftmostZero(2 * node + 1, mid + 1, end);
    }
}
// index:   0   1   2   3   4
// state:   2   1   0  -1   0
// Segment Tree 結構：
//                 [0,4]
//             min=-1 max=2
//            /              \
//        [0,2]            [3,4]
//     min=0 max=2       min=-1 max=0
//      /     \           /      \
//  [0,1]    [2,2]    [3,3]    [4,4]
public class Solution {
    public int longestBalanced(int[] nums) {
        int n = nums.length;
        Map<Integer, Integer> prev = new HashMap<>();

        SegmentTree st = new SegmentTree(n);
        int res = 0;

        for (int r = 0; r < n; r++) {
            int v = nums[r];
            // 轉成奇偶
            int val = (v % 2 == 0) ? 1 : -1;
            // 就必須把之前那次貢獻扣掉
            if (prev.containsKey(v)) {
                st.updateRange(1, 0, n - 1, 0, prev.get(v), -val);
            }

            st.updateRange(1, 0, n - 1, 0, r, val);
            prev.put(v, r);

            int left = st.findLeftmostZero(1, 0, n - 1);
            if (left != -1 && left <= r) {
                res = Math.max(res, r - left+ 1);
            }
        }

        return res;
    }
}
```

