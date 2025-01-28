# 875. Koko Eating Bananas

Methods: Binary Search
Difficulty: Medium

Koko loves to eat bananas. There are `n` piles of bananas, the `ith` pile has `piles[i]` bananas. The guards have gone and will come back in `h` hours.

Koko can decide her bananas-per-hour eating speed of `k`. Each hour, she chooses some pile of bananas and eats `k` bananas from that pile. If the pile has less than `k` bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return *the minimum integer* `k` *such that she can eat all the bananas within* `h` *hours*.

**Example 1:**

```
Input: piles = [3,6,7,11], h = 8
Output: 4

```

**Example 2:**

```
Input: piles = [30,11,23,4,20], h = 5
Output: 30

```

**Example 3:**

```
Input: piles = [30,11,23,4,20], h = 6
Output: 23

```

**Constraints:**

- `1 <= piles.length <= 104`
- `piles.length <= h <= 109`
- `1 <= piles[i] <= 109`

```java
class Solution {
    public int minEatingSpeed(int[] piles, int h) {//找最小k k可能範圍(大 : pile中最大,小 : 1) binary search
        Arrays.sort(piles);//找最大的pile;
        int left = 1;
        int right = piles[piles.length - 1];
        long k = 0;
        while(left <= right){
            int mid = left + (right - left) / 2;
            for(int i : piles){
                k += i / mid;
                if(i % mid != 0)
                    k++;
            }
            if(k <= h){//當所需時間在guard回來前
                right = mid -1;
            }else{//來不及
                left = mid + 1;
            }
            k = 0;
        }
        return left;
    }
}
```