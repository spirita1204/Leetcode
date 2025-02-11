# 912.Sort an Array

Methods: Sort
Difficulty: Medium

Given an array of integers `nums`, sort the array in ascending order and return it.

You must solve the problem **without using any built-in** functions in `O(nlog(n))` time complexity and with the smallest space complexity possible.

**Example 1:**

```
Input: nums = [5,2,3,1]
Output: [1,2,3,5]
Explanation: After sorting the array, the positions of some numbers are not changed (for example, 2 and 3), while the positions of other numbers are changed (for example, 1 and 5).

```

**Example 2:**

```
Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
Explanation: Note that the values of nums are not necessairly unique.
```

採用merge sort (O(N log N) 

**Divide (N-1次)**

 **Conquer (log N)**

[演算法筆記(一) | Merge sort and Insert sort實作in Java](https://medium.com/codeda/演算法筆記-一-merge-sort-and-insert-sort實作in-java-cb3ca6f7e22b)

```java
class Solution {
    public int[] sortArray(int[] nums) {
        return sortArray(nums, 0, nums.length - 1);
    }
    public int[] sortArray(int[] nums, int arrStartIndex, int arrEndIndex){
        if (arrStartIndex < arrEndIndex) {
            int middleIndex = (arrStartIndex + arrEndIndex) / 2;

            // 這邊使用 Divide and Conquer，將複雜的問題分成兩個或更多的相同或相似的子問題
            sortArray(nums, arrStartIndex, middleIndex);
            sortArray(nums, middleIndex + 1, arrEndIndex);

            merge(nums, arrStartIndex, middleIndex, arrEndIndex);
        }
        return nums;
    }
    public void merge(int[] arr, int arrStartIndex, int middleIndex, int arrEndIndex) {
        // 計算左右兩陣列的長度
        int leftArrLength = middleIndex - arrStartIndex + 1;
        int rightArrLength = arrEndIndex - middleIndex;

        // 製作左右兩陣列
        int LeftArr[] = new int[leftArrLength];
        int RightArr[] = new int[rightArrLength];

        // 將資料放入左右兩陣列
        for (int i = 0; i < leftArrLength; i++) {
            // 從 arrStarIndex 開始
            LeftArr[i] = arr[arrStartIndex + i];
        }

        for (int j = 0; j < rightArrLength; j++) {
            // 從 middleIndex 開始
            RightArr[j] = arr[middleIndex + 1 + j];
        }

        // 接著要開始遍歷左右陣列準備合併，於是要先建立兩個陣列的 index
        int leftArrIndex = 0, rightArrIndex = 0;
        // 合併後的大陣列 index
        int mergedArrIndex = arrStartIndex;

        while (leftArrIndex < leftArrLength && rightArrIndex < rightArrLength) {
            // 比較左右兩陣列的數值，數值小的放入合併後的陣列
            if (LeftArr[leftArrIndex] <= RightArr[rightArrIndex]) {
                arr[mergedArrIndex] = LeftArr[leftArrIndex];
                leftArrIndex++;
            } else {
                arr[mergedArrIndex] = RightArr[rightArrIndex];
                rightArrIndex++;
            }

            mergedArrIndex++;
        }

        // 將剩餘的數值放入合併後的陣列，剩餘數值會將大於合併後的陣列內的任一元素
        while (leftArrIndex < leftArrLength) {
            arr[mergedArrIndex] = LeftArr[leftArrIndex];
            leftArrIndex++;
            mergedArrIndex++;
        }

        // 將剩餘的數值放入合併後的陣列，剩餘數值會將大於合併後的陣列內的任一元素
        while (rightArrIndex < rightArrLength) {
            arr[mergedArrIndex] = RightArr[rightArrIndex];
            rightArrIndex++;
            mergedArrIndex++;
        }
    }
}
```

Quick sort  (O(N log N) 

[Comparison Sort: Quick Sort(快速排序法)](https://alrightchiu.github.io/SecondRound/comparison-sort-quick-sortkuai-su-pai-xu-fa.html)

[https://www.youtube.com/watch?v=AsQW27DT82I](https://www.youtube.com/watch?v=AsQW27DT82I)

```java
class Solution {
    public int[] sortArray(int[] nums) {
        //return sortArrayMerge(nums, 0, nums.length - 1);
        int a = nums[0],count = 0;
        for(int i : nums){// 因為run不會TLE但submit會 所以補上
            if(a == i) count++;
        }
        if(count == nums.length) return nums;
        quickSort(nums, 0, nums.length - 1);
        return nums;
    }   
    public void quickSort(int[] nums, int l, int r) {
        if (l >= r) return;
        int mid = partition(nums, l, r);//左側皆小於 右側皆大於
        quickSort(nums, l, mid);
        quickSort(nums, mid + 1, r);
    }
    public int partition(int[] nums, int l, int r) {
        int pivot = l;//pivot設在最左
        while (l < r) {
            while (l < r && nums[r] >= nums[pivot]) r--;
            while (l < r && nums[l] <= nums[pivot]) l++;
            int tmp = nums[r];
            if(l == r){//碰到          
                nums[r] = nums[pivot];
                nums[pivot] = tmp;
            }else{//還沒碰到
                nums[r] = nums[l];
                nums[l] = tmp;
            }
        }
        return l; //回傳中間值
    }
```

## 2024/07/25 重寫merge sort

```java
class Solution {
    public int[] sortArray(int[] nums) {// merge sort
        return sortArray(nums, 0, nums.length - 1);
    }

    private int[] sortArray(int[] nums, int start, int end){
        if(start < end) {
            // Divide 
            int mid = (start + end) / 2;
            sortArray(nums, start, mid);
            sortArray(nums, mid + 1, end);
            // Conquer
            merge(nums, start, mid, end);
        }
        return nums;// 排序完的nums
    }

    private void merge(int[] nums, int start, int mid, int end) {
        // 1.將兩陣列合併
        // 2.將彼此剩餘加入
        int len1 = mid - start + 1;
        int len2 = end - mid;

        int[] arr1 = new int[len1];
        int[] arr2 = new int[len2];
        // 填充
        for(int i = 0; i < len1; i++) 
            arr1[i] = nums[start + i];
        for(int i = 0; i < len2; i++) 
            arr2[i] = nums[mid + 1 + i];
        // 合併
        int i = 0;// 指到arr1
        int j = 0;// 指到arr2
        int m = start;// 合併陣列指標
        while(i < len1 && j < len2) {
            if(arr1[i] < arr2[j]) 
                nums[m++] = arr1[i++];
            else 
                nums[m++] = arr2[j++];
        }
        while(i < len1) {
            nums[m++] = arr1[i++];
        }
        while(j < len2) {
            nums[m++] = arr2[j++];
        }
    }
}
```