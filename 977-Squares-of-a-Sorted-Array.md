# 977. Squares of a Sorted Array

Methods: Pointer
Difficulty: Easy

Given an integer array `nums` sorted in **non-decreasing** order, return *an array of **the squares of each number** sorted in non-decreasing order*.

**Example 1:**

```
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].

```

**Example 2:**

```
Input: nums = [-7,-3,2,3,11]
Output: [4,9,9,49,121]

```

**Constraints:**

- `1 <= nums.length <= 104`
- `104 <= nums[i] <= 104`
- `nums` is sorted in **non-decreasing** order.

**Follow up:**

Squaring each element and sorting the new array is very trivial, could you find an

```
O(n)
```

solution using a different approach?

```jsx
class Solution {
    public int[] sortedSquares(int[] nums) {
        int front = 0; //比較頭尾
        int end = nums.length - 1;
        int[] res = new int[nums.length];

        for(int i = nums.length - 1; i >= 0; i--){
            if(Math.abs(nums[front]) > Math.abs(nums[end])){
                res[i] = nums[front]* nums[front];
                front++;
            }else{
                res[i] = nums[end]* nums[end];
                end--;
            }
        }
        return res;
    }
}
```