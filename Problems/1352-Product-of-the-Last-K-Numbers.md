# 1352. Product of the Last K Numbers  

  Methods: Prefix Sum </br> Difficulty: Medium </br> </br>Design an algorithm that accepts a stream of integers and retrieves the product of the last `k` integers of the stream.

Implement the `ProductOfNumbers` class:

- `ProductOfNumbers()` Initializes the object with an empty stream.
- `void add(int num)` Appends the integer `num` to the stream.
- `int getProduct(int k)` Returns the product of the last `k` numbers in the current list. You can assume that always the current list has at least `k` numbers.
The test cases are generated so that, at any time, the product of any contiguous sequence of numbers will fit into a single 32-bit integer without overflowing.

**Example:**

```plain text
Input
["ProductOfNumbers","add","add","add","add","add","getProduct","getProduct","getProduct","add","getProduct"]
[[],[3],[0],[2],[5],[4],[2],[3],[4],[8],[2]]

Output
[null,null,null,null,null,null,20,40,0,null,32]

Explanation
ProductOfNumbers productOfNumbers = new ProductOfNumbers();
productOfNumbers.add(3);        // [3]
productOfNumbers.add(0);        // [3,0]
productOfNumbers.add(2);        // [3,0,2]
productOfNumbers.add(5);        // [3,0,2,5]
productOfNumbers.add(4);        // [3,0,2,5,4]
productOfNumbers.getProduct(2); // return 20. The product of the last 2 numbers is 5 * 4 = 20
productOfNumbers.getProduct(3); // return 40. The product of the last 3 numbers is 2 * 5 * 4 = 40
productOfNumbers.getProduct(4); // return 0. The product of the last 4 numbers is 0 * 2 * 5 * 4 = 0
productOfNumbers.add(8);        // [3,0,2,5,4,8]
productOfNumbers.getProduct(2); // return 32. The product of the last 2 numbers is 4 * 8 = 32

```

**Constraints:**

- `0 <= num <= 100`
- `1 <= k <= 4 * 104`
- At most `4 * 104` calls will be made to `add` and `getProduct`.
- The product of the stream at any point in time will fit in a **32-bit** integer.
**Follow-up:**

Can you implement **both **GetProduct and Add to work in O(1) time complexity instead of O(k) time complexity?

```java
class ProductOfNumbers {
    //   3 0 2  5  4
    // prefix product
    // 1 3 1 2 10 40
    int index = 1;
    int lastZeroPos = 0;
    List<Integer> prefixProduct;
    public ProductOfNumbers() {
       prefixProduct = new ArrayList<>();
       prefixProduct.add(1);
    }
    
    public void add(int num) {
        if(num == 0) {
            lastZeroPos = ++index;// 紀錄最後0出現位置
            prefixProduct.add(1);
            return;
        }
        int pre = prefixProduct.get(index - 1);
        prefixProduct.add(pre * num);
        index++;
    }
    
    public int getProduct(int k) {
        if(index - k < lastZeroPos)
            return 0;
        return prefixProduct.get(index - 1) / prefixProduct.get(index - k - 1);
    }
}

/**
 * Your ProductOfNumbers object will be instantiated and called as such:
 * ProductOfNumbers obj = new ProductOfNumbers();
 * obj.add(num);
 * int param_2 = obj.getProduct(k);
 */
```

