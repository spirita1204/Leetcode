# 3306. Count of Substrings Containing Every Vowel and K Consonants II  

  Methods: Pointer,Binary Search </br> Difficulty: Medium++ </br> </br>You are given a string `word` and a **non-negative** integer `k`.

Return the total number of substrings of `word` that contain every vowel (`'a'`, `'e'`, `'i'`, `'o'`, and `'u'`) **at least** once and **exactly** `k` consonants.

**Example 1:**

**Input:** word = "aeioqq", k = 1

**Output:** 0

**Explanation:**

There is no substring with every vowel.

---

**Example 2:**

**Input:** word = "aeiou", k = 0

**Output:** 1

**Explanation:**

The only substring with every vowel and zero consonants is `word[0..4]`, which is `"aeiou"`.

---

**Example 3:**

**Input:** word = "ieaouqqieaouqq", k = 1

**Output:** 3

**Explanation:**

The substrings with every vowel and one consonant are:

---

- `word[0..5]`, which is `"ieaouq"`.
- `word[6..11]`, which is `"qieaou"`.
- `word[7..12]`, which is `"ieaouq"`.
**Constraints:**

- `5 <= word.length <= 2 * 105`
- `word` consists only of lowercase English letters.
- `0 <= k <= word.length - 5`
---

Hint 1

We can use sliding window and binary search.

---

Hint 2

For each index `r`, find the maximum `l` such that both conditions are satisfied using binary search.

```java
class Solution {
    public long countOfSubstrings(String word, int k) {
        String vowels = "aeiou"; // 定義母音
        int left = 0, mid = 0; // 兩個指標，控制滑動視窗
        int uniqueVowelCount = 0; // 當前視窗內不同母音的數量
        int[] frequency = new int[6]; // 記錄視窗內的母音與子音數量
        int[] tempFrequency = new int[6]; // 幫助計算有效子字串
        long totalSubstrings = 0; // 儲存符合條件的子字串數量

        // 使用 right 指標遍歷字串
        for (int right = 0; right < word.length(); right++) {
            int vowelIndex = vowels.indexOf(word.charAt(right)) + 1; // 取得字母索引（母音為1~5，子音為0）
            frequency[vowelIndex]++; // 更新該字母在視窗內的頻率

            // 如果是新的母音，增加計數
            if (vowelIndex > 0 && frequency[vowelIndex] == 1) 
                uniqueVowelCount++;
            // 當子音數超過 k，縮小視窗
            while (frequency[0] > k) {
                int leftVowelIndex = vowels.indexOf(word.charAt(left)) + 1;
                frequency[leftVowelIndex]--; // 移除最左端字母

                // 若母音數減少至 0，則減少計數
                if (leftVowelIndex > 0 && frequency[leftVowelIndex] == 0) 
                    uniqueVowelCount--;
                left++; // 移動左指標
            }
            // 檢查當前視窗是否符合條件
            if (uniqueVowelCount == 5 && frequency[0] == k) {
                // 若 mid 指標落後於 left，則重置
                if (mid < left) {
                    mid = left;
                    Arrays.fill(tempFrequency, 0); // 清空暫存頻率
                }
                // 移動 mid 指標，計算有效子字串
                while (true) {
                    int midVowelIndex = vowels.indexOf(word.charAt(mid)) + 1;
                    // 若遇到子音或母音數用盡，則停止擴展
                    if (midVowelIndex == 0 || frequency[midVowelIndex] - tempFrequency[midVowelIndex] == 1) 
                        break;
                    tempFrequency[midVowelIndex]++; // 記錄母音計數
                    mid++;
                }
                // 計算所有符合條件的子字串
                totalSubstrings += mid - left + 1;
            }
        }
        return totalSubstrings;
    }
}
```

