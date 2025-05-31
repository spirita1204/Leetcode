# 307. Range Sum Query - Mutable  

  Data Structure: Binary Indexed Tree(Fenwick Tree) </br> Difficulty: Medium </br> </br>Given an integer array `nums`, handle multiple queries of the following types:

1. **Update** the value of an element in `nums`.
1. Calculate the **sum** of the elements of `nums` between indices `left` and `right` **inclusive** where `left <= right`.
Implement the `NumArray` class:

- `NumArray(int[] nums)` Initializes the object with the integer array `nums`.
- `void update(int index, int val)` **Updates** the value of `nums[index]` to be `val`.
- `int sumRange(int left, int right)` Returns the **sum** of the elements of `nums` between indices `left` and `right` **inclusive** (i.e. `nums[left] + nums[left + 1] + ... + nums[right]`).
**Example 1:**

```plain text
Input
["NumArray", "sumRange", "update", "sumRange"]
[[[1, 3, 5]], [0, 2], [1, 2], [0, 2]]
Output
[null, 9, null, 8]

Explanation
NumArray numArray = new NumArray([1, 3, 5]);
numArray.sumRange(0, 2); // return 1 + 3 + 5 = 9
numArray.update(1, 2);   // nums = [1, 2, 5]
numArray.sumRange(0, 2); // return 1 + 2 + 5 = 8
```

**Constraints:**

- `1 <= nums.length <= 3 * 104`
- `100 <= nums[i] <= 100`
- `0 <= index < nums.length`
- `100 <= val <= 100`
- `0 <= left <= right < nums.length`
- At most `3 * 104` calls will be made to `update` and `sumRange`.
```java
class NumArray {
    BIT bit;
    int[] nums;

    public NumArray(int[] nums) {
        this.nums = nums;
        bit = new BIT(nums.length);

        for (int i = 0; i < nums.length; i++)
            bit.addValue(i + 1, nums[i]);
    }

    public void update(int index, int val) {
        int diff = val - nums[index]; 
        bit.addValue(index + 1, diff); 
        nums[index] = val;
    }

    public int sumRange(int left, int right) {
        return bit.getSum(right + 1) - bit.getSum(left);
    }
}

class BIT {
    int[] bit;

    BIT(int size) {
        bit = new int[size + 1];
    }

    int getSum(int idx) { // Get sum in range [1..idx]
        int sum = 0;

        while (idx > 0) {
            sum += bit[idx];
            idx -= idx & (-idx);
        }
        return sum;
    }

    int getSumRange(int left, int right) { // left, right inclusive
        return getSum(right) - getSum(left - 1);
    }

    void addValue(int idx, int val) {
        while (idx < bit.length) {
            bit[idx] += val;
            idx += idx & (-idx);
        }
    }
}
```

