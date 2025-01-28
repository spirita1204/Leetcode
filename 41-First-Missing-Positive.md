# 41. First Missing Positive

Methods: Sort
Difficulty: Hard

Hard

Topics

Companies

Hint

Given an unsorted integer array `nums`. Return the *smallest positive integer* that is *not present* in `nums`.

You must implement an algorithm that runs in `O(n)` time and uses `O(1)` auxiliary space.

**Example 1:**

```
Input: nums = [1,2,0]
Output: 3
Explanation: The numbers in the range [1,2] are all in the array.

```

**Example 2:**

```
Input: nums = [3,4,-1,1]
Output: 2
Explanation: 1 is in the array but 2 is missing.

```

**Example 3:**

```
Input: nums = [7,8,9,11,12]
Output: 1
Explanation: The smallest positive integer 1 is missing.

```

**Constraints:**

- `1 <= nums.length <= 105`
- `231 <= nums[i] <= 231 - 1`

### O(N) O(1) Space

```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        // Index sorting O(N) time complexity
        // [3,1,2,5,4]
        int len = nums.length;
        int i = 0;
        while (i < len) {
            // 已在自己位置 不用處理
            if(nums[i] == i + 1 || nums[i] <= 0 || nums[i] > len) i++;
            // 交換到自己位置
            else if(nums[nums[i] - 1] != nums[i]) swap(nums, i, nums[i] - 1);
            // [0,2,2,1,1] 避免重複情況無法交換
            else i++;
        }
        // 對排好序 查詢
        i = 0;
        while (i < len && nums[i] == i + 1)
            i++;

        return i + 1;
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

### NLogN

```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        Arrays.sort(nums);
        int cnt = 1;
        for(int i: nums) {
            if(i <= 0 || i < cnt) continue;
            if(i == cnt) cnt++;
            else return cnt;
        }
        return cnt;
    }
}
```

### O(N) O(1) Space

```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        boolean[] arr = new boolean[100001];

        for(int i: nums) {
            if(i <= 0 || i >= 100001) continue;
            arr[i] = true;
        }
        for(int i = 1; i< arr.length; i++) 
            if(!arr[i]) return i;
        return 100001;
    }
}
```