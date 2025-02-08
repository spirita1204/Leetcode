# 2349. Design a Number Container System  

  Data Structure: Hash Table </br> Difficulty: Medium </br> </br>Design a number container system that can do the following:

- **Insert **or **Replace** a number at the given index in the system.
- **Return **the smallest index for the given number in the system.
Implement the `NumberContainers` class:

- `NumberContainers()` Initializes the number container system.
- `void change(int index, int number)` Fills the container at `index` with the `number`. If there is already a number at that `index`, replace it.
- `int find(int number)` Returns the smallest index for the given `number`, or `1` if there is no index that is filled by `number` in the system.
**Example 1:**

```plain text
Input
["NumberContainers", "find", "change", "change", "change", "change", "find", "change", "find"]
[[], [10], [2, 10], [1, 10], [3, 10], [5, 10], [10], [1, 20], [10]]
Output
[null, -1, null, null, null, null, 1, null, 2]

Explanation
NumberContainers nc = new NumberContainers();
nc.find(10); // There is no index that is filled with number 10. Therefore, we return -1.
nc.change(2, 10); // Your container at index 2 will be filled with number 10.
nc.change(1, 10); // Your container at index 1 will be filled with number 10.
nc.change(3, 10); // Your container at index 3 will be filled with number 10.
nc.change(5, 10); // Your container at index 5 will be filled with number 10.
nc.find(10); // Number 10 is at the indices 1, 2, 3, and 5. Since the smallest index that is filled with 10 is 1, we return 1.
nc.change(1, 20); // Your container at index 1 will be filled with number 20. Note that index 1 was filled with 10 and then replaced with 20.
nc.find(10); // Number 10 is at the indices 2, 3, and 5. The smallest index that is filled with 10 is 2. Therefore, we return 2.

```

**Constraints:**

- `1 <= index, number <= 109`
- At most `105` calls will be made **in total** to `change` and `find`.
```java
class NumberContainers {
    Map<Integer, TreeSet<Integer>> hm; // number -> set<index>
    Map<Integer, Integer> hm2; // index -> number

    public NumberContainers() {
        hm = new HashMap<>();
        hm2 = new HashMap<>();
    }  

    public void change(int index, int number) {
        if (!hm.containsKey(number)) {
            hm.put(number, new TreeSet<>());
        } 

        Integer prevNumber = hm2.get(index);

        if (prevNumber != null) {
            hm.get(prevNumber).remove(index); // 修正
        } 

        hm.get(number).add(index);
        hm2.put(index, number);
    }

    public int find(int number) {
        if (!hm.containsKey(number) || hm.get(number).isEmpty())
            return -1;
        return hm.get(number).first();
    }
}


/**
 * Your NumberContainers object will be instantiated and called as such:
 * NumberContainers obj = new NumberContainers();
 * obj.change(index,number);
 * int param_2 = obj.find(number);
 */
```

最佳化作法

```java
class NumberContainers {

    HashMap<Integer,PriorityQueue<Integer>> res;
    HashMap<Integer,Integer> index_val;

    public NumberContainers() {
        res = new HashMap<>();
        index_val = new HashMap<>();
    }
    
    public void change(int index, int number) {

        if(index_val.containsKey(index)){
            int num = index_val.get(index);
            if(num == number){
                return ;
            }

            res.get(num).remove(index);
        }

        res.computeIfAbsent(number, k-> new PriorityQueue<>()).offer(index);
        index_val.put(index, number);
    }
    
    public int find(int number) 
    {
        PriorityQueue<Integer> pq = res.getOrDefault(number, new PriorityQueue<>());
        if(pq.size() == 0)
        {
            return -1;
        }
        return pq.peek();
    }
}

/**
 * Your NumberContainers object will be instantiated and called as such:
 * NumberContainers obj = new NumberContainers();
 * obj.change(index,number);
 * int param_2 = obj.find(number);
 */
```

### `**PriorityQueue**`** 比 **`**TreeSet**`** 更快的主要原因**

### **(1) **`**PriorityQueue**`** 只維護「堆頂最小值」，而 **`**TreeSet**`** 維護整個排序結構**

- `TreeSet` 本質上是一個 **紅黑樹 (Red-Black Tree)**，它**維護整個集合的順序**，所以在插入或刪除時需要調整平衡。
- `PriorityQueue` 是 **最小堆 (Min Heap)**，它**只確保堆頂是最小的**，不需要維護完整的排序結構，因此 **增刪的實際效率通常優於 **`**TreeSet**`。
### **(2) **`**find()**`** 操作的優化**

- `TreeSet.first()` 直接返回最小索引，時間複雜度是 `O(1)`。
- `PriorityQueue.peek()` 也是 `O(1)`，但由於 `PriorityQueue` 內部結構比 `TreeSet` 更簡單，因此 `peek()` 的實際執行速度可能更快。
### **(3) **`**PriorityQueue**`** 適合「頻繁查詢最小值」的場景**

- 你的 `find()` 方法只是查詢最小索引，而不會頻繁移除非堆頂的元素。
- `**PriorityQueue**`** 更適合這種場景，因為它只確保最小值在堆頂**，所以 `peek()` 很快。
```java
Heap is apparently much faster - once you realize that you don't need to clean up overwritten values at each change() if you validate during find().
```

