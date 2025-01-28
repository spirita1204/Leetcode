# 283. Move Zeroes

Methods: Pointer
Difficulty: Easy

**Easy**

13.1K

330

Given an integer array `nums`, move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Note** that you must do this in-place without making a copy of the array.

**Example 1:**

```
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]

```

**Example 2:**

```
Input: nums = [0]
Output: [0]

```

**Constraints:**

- `1 <= nums.length <= 104`
- `231 <= nums[i] <= 231 - 1`

**Follow up:**

Could you minimize the total number of operations done?

```jsx
class Solution {
    public void moveZeroes(int[] nums) {
        
        int p1 = 0;// 紀錄要換位置
        int p2 = 0;// 去找非0來換
        while(p1 < nums.length && p2 < nums.length){
            if(nums[p1] == 0){
                if(nums[p2] == 0) 
                    p2++;
                else{ //找到要交換的非0
                    int tmp = nums[p1];
                    nums[p1] = nums[p2];
                    nums[p2] = tmp;
                    p1++;
                }
            }else{
                p1++;
                p2++;
            }
        }
    }
}
```