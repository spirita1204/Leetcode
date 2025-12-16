# 632. Smallest Range Covering Elements from K Lists  

  Methods: Pointer </br> Difficulty: Hard </br> </br>You have `k` lists of sorted integers in **non-decreasing order**. Find the **smallest** range that includes at least one number from each of the `k` lists.

We define the range `[a, b]` is smaller than range `[c, d]` if `b - a < d - c` **or** `a < c` if `b - a == d - c`.

**Example 1:**

```plain text
Input: nums = [[4,10,15,24,26],[0,9,12,20],[5,18,22,30]]
Output: [20,24]
Explanation:
List 1: [4, 10, 15, 24,26], 24 is in range [20,24].
List 2: [0, 9, 12, 20], 20 is in range [20,24].
List 3: [5, 18, 22, 30], 22 is in range [20,24].

```

**Example 2:**

```plain text
Input: nums = [[1,2,3],[1,2,3],[1,2,3]]
Output: [1,1]

```

**Constraints:**

- `nums.length == k`
- `1 <= k <= 3500`
- `1 <= nums[i].length <= 50`
- `105 <= nums[i][j] <= 105`
- `nums[i]` is sorted in **non-decreasing** order.
```java
class Solution {
    public int[] smallestRange(List<List<Integer>> nums) {
        int[] res = new int[2];
        int size = 0;
        for (int i = 0; i < nums.size(); i++) 
            size += nums.get(i).size();
        Pair[] pairs = new Pair[size];
        // 合併成一個陣列
        for (int idx = 0, i = 0; i < nums.size(); i++) {
            for (int num : nums.get(i)) {
                pairs[idx++] = new Pair(num, i);// 數字, 哪個group
            }
        }
        Arrays.sort(pairs, (a, b) -> a.val - b.val);
        int left = 0, right = 0;// 
        Map<Integer, Integer> hm = new HashMap<>();
        int cnt = 0, diff = Integer.MAX_VALUE;

        while(right < size) {
            if(hm.get(pairs[right].idx) == null || hm.get(pairs[right].idx) == 0) 
                cnt++;
            hm.put(pairs[right].idx, hm.getOrDefault(pairs[right].idx, 0) + 1);// group重複idx直接覆蓋
            while (cnt == nums.size() && left <= right) {// 更小diff
                if (diff > pairs[right].val - pairs[left].val) {
                    diff = pairs[right].val - pairs[left].val;
                    res[0] = pairs[left].val;
                    res[1] = pairs[right].val;
                } 
                if (hm.get(pairs[left].idx) == 1) {
                    cnt--;
                }
                hm.put(pairs[left].idx, hm.get(pairs[left].idx) - 1);
                left++;// 向左移動
            }
            right++;
        }
        return res;
    }
}
class Pair {
    int val;
    int idx;

    Pair(int val, int idx) {
        this.val = val;
        this.idx = idx;
    }
}
```

