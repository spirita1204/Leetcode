# 605. Can Place Flowers

Methods: Basic logic
Difficulty: Easy

**605. Can Place Flowers**

**Easy**

3.6K

733

You have a long flowerbed in which some of the plots are planted, and some are not. However, flowers cannot be planted in **adjacent** plots.

Given an integer array `flowerbed` containing `0`'s and `1`'s, where `0` means empty and `1` means not empty, and an integer `n`, return *if* `n` new flowers can be planted in the `flowerbed` without violating the no-adjacent-flowers rule.

**Example 1:**

```
Input: flowerbed = [1,0,0,0,1], n = 1
Output: true

```

**Example 2:**

```
Input: flowerbed = [1,0,0,0,1], n = 2
Output: false

```

**Constraints:**

- `1 <= flowerbed.length <= 2 * 104`
- `flowerbed[i]` is `0` or `1`.
- There are no two adjacent flowers in `flowerbed`.
- `0 <= n <= flowerbed.length`

```java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int count = 0;
        for(int i = 0; i < flowerbed.length; i++){
            if(flowerbed[i] == 1){
                i++;
            }else{//確認是否可植花
                if(i + 1 <= flowerbed.length - 1 && flowerbed[i+1] != 1){//當還沒到底
                    count++;
                    i++;
                    
                }else if(i == flowerbed.length - 1){//到底
                    count++;
                    i++;
                }
            }
        }
        System.out.print(count);
        return (n <= count) ? true : false;
    }
}
```