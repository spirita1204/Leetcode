# 3347. Maximum Frequency of an Element After Performing Operations II  

  Methods: Sweep line </br> Data Structure: Hash Table </br> Difficulty: Hard </br> </br>You are given an integer array `nums` and two integers `k` and `numOperations`.

You must perform an **operation** `numOperations` times on `nums`, where in each operation you:

- Select an index `i` that was **not** selected in any previous operations.
- Add an integer in the range `[-k, k]` to `nums[i]`.
Return the **maximum** possible frequency of any element in `nums` after performing the **operations**.

**Example 1:**

**Input:** nums = [1,4,5], k = 1, numOperations = 2

**Output:** 2

**Explanation:**

We can achieve a maximum frequency of two by:

- Adding 0 to `nums[1]`, after which `nums` becomes `[1, 4, 5]`.
- Adding -1 to `nums[2]`, after which `nums` becomes `[1, 4, 4]`.
**Example 2:**

**Input:** nums = [5,11,20,20], k = 5, numOperations = 1

**Output:** 2

**Explanation:**

We can achieve a maximum frequency of two by:

- Adding 0 to `nums[1]`.
**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 109`
- `0 <= k <= 109`
- `0 <= numOperations <= nums.length`
```java
class Solution {
    public int maxFrequency(int[] nums, int k, int numOperations) {
        Map<Integer, Integer> pointsCover = new HashMap<>();// 有幾個 nums[i] 可以被調整成 X
        Map<Integer, Integer> cntPoints = new HashMap<>();// 原本就等於 X 的數量
        Set<Integer> points = new TreeSet<>(); // TreeSet to keep points sorted

        for (int num : nums) {
            cntPoints.put(num, cntPoints.getOrDefault(num, 0) + 1);
            pointsCover.put(num - k, pointsCover.getOrDefault(num - k, 0) + 1);
            pointsCover.put(num + k + 1, pointsCover.getOrDefault(num + k + 1, 0) - 1);
            points.add(num);
            points.add(num - k);
            points.add(num + k + 1);
        }

        int res = 0;
        int pointsCoverThisPoint = 0;// 能變成 point 的「總元素數」

        for (int point : points) {
            pointsCoverThisPoint += pointsCover.getOrDefault(point, 0);
            res = Math.max(res, cntPoints.getOrDefault(point, 0) + 
                        // 「需要操作」才能變成 point 的元素數
                        Math.min(pointsCoverThisPoint - cntPoints.getOrDefault(point, 0), numOperations));
        }

        return res;
    }
}
```

