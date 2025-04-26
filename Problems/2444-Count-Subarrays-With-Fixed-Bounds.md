# 2444. Count Subarrays With Fixed Bounds  

  Methods: Pointer,Greedy </br> Difficulty: Hard </br> </br>![Image](https://prod-files-secure.s3.us-west-2.amazonaws.com/81bfe8e8-c2fe-4d29-8949-0ba3cf293f0f/7ab8a4bd-ff1b-4f1c-afa0-b4a5226f3b77/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QVXTE3OJ%2F20250426%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250426T054800Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEKb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIFp3z4je%2BWMYMTbYZFQWdi4LJguN1S2YZ9rTwqWt%2BMSEAiEAkoZIe9JJif%2BYEfOdYFb%2BWI6AN2NSmz95lZTunyqlOAcq%2FwMIPxAAGgw2Mzc0MjMxODM4MDUiDIfbgwnYbPOxiHAxdSrcAwvTLWNDBzGXMU2s9K2qkJMn5H3MZu1CRciT1YiW%2BiWvFa1qnFv1iyUq1LAs1uxU%2FeC%2BVRTpQOtsmoxTmrgDXYhWzHw%2F639XbVhqhDwP3MJq%2BftKfDB7VcAXoCC46puYSe3U8kCeWOfdSfHC5J3dLjOUiUaQvyEivk7p17fpjcW12R2JRORx6jF0l%2BVeGgUOQFYY%2FUIKg6%2FQ5vSoz3OWjzL5BCBNLSOMf7O9CqU9am4x%2B50Notr6zwdN6Rip6KB5Ebpu0qdoOVo7dg2od%2F%2F10%2FBP463OV%2BiGWUIO3EH%2FKClSn2bq5j2HXc2ZDH06rfLK1m6whh3vhBuLyDMNDEudtlCBX6brIz9uTaWJN1RR56NbhnlWWZ5lMNU8ebduQzvaOzVhPHee%2BXnk3qw0%2FDMluLG%2FYm58U7rrOMzOa2kz2Z5lOAFxrHBVKm2E3b1pWtAgDEo6%2FaFD1sbZaBfvQIApx4upLOArI4LmspavmAfO8Ly2ht58MyQ7mrwIaKUxk1PCuXCZB7TDQ9GaZuYxTykzqelda7OFEZM8QTkVb2mo6aPIWbJ%2BS%2Fld%2BJyeojWFNEoFSJ%2FL%2Fw5DS8xl4nIko55fZYgi55JPhEYW46h2NWo2nHfQmTFb6A2GBELTaiN7MJzkscAGOqUBsQ9r5NnBxLXBnQehpqj1KFB3SZtm5RcUZIdofxOJ%2BfeU6%2BEt2AMax%2FgtvxW5VKY663qrQW0CWzBTqm0KayP1JFOZQV1ooplHVvCScpoow20qNNI2ObqZbdUusuZNRKeKgAgKfbGExlc%2BU0fRo3r2xJT4TdavPTNZc4xEgyFTPS%2Ba573uz7C3a%2FhnXiBLqotvgymCV7eGvWVcc%2FOBLHD2oAFVP3VD&X-Amz-Signature=7e05f58d00a92693c50463b1ea14c35b4fa54fb44adcf797c921c9f57f76f226&X-Amz-SignedHeaders=host&x-id=GetObject)

You are given an integer array `nums` and two integers `minK` and `maxK`.

A **fixed-bound subarray** of `nums` is a subarray that satisfies the following conditions:

- The **minimum** value in the subarray is equal to `minK`.
- The **maximum** value in the subarray is equal to `maxK`.
Return *the ****number**** of fixed-bound subarrays*.

A **subarray** is a **contiguous** part of an array.

**Example 1:**

```plain text
Input: nums = [1,3,5,2,7,5], minK = 1, maxK = 5
Output: 2
Explanation: The fixed-bound subarrays are [1,3,5] and [1,3,5,2].
```

**Example 2:**

```plain text
Input: nums = [1,1,1,1], minK = 1, maxK = 1
Output: 10
Explanation: Every subarray of nums is a fixed-bound subarray. There are 10 possible subarrays.
```

```java
class Solution {
    public long countSubarrays(int[] nums, int minK, int maxK) {
        int left = 0;// 定義可以到左的點
        int lastMin = -1, lastMax = -1;
        int n = nums.length;
        long res = 0L;
        
        for (int right = 0; right < n; right++) {
            if (nums[right] < minK || nums[right] > maxK) {// 超出邊界
                lastMin = -1;
                lastMax = -1;
                left = right + 1;
            }
            if (nums[right] == minK)
                lastMin = right;
            if (nums[right] == maxK)
                lastMax = right;
            // 當min max都有 取他們最小(Math.min)代表最少要有subarr的長度 減掉可以繼續往左延伸的距離 就是subarr可以的數量
            if (lastMin != -1 && lastMax != -1)
                res += Math.min(lastMin, lastMax) - left + 1;
        }
        return res;
    }
}
```

