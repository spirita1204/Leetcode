# 155. Min Stack

Methods: Basic logic
Difficulty: Medium

Medium

Topics

Companies

Hint

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with `O(1)` time complexity for each function.

**Example 1:**

```
Input
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

Output
[null,null,null,null,-3,null,0,-2]

Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2

```

**Constraints:**

- `231 <= val <= 231 - 1`
- Methods `pop`, `top` and `getMin` operations will always be called on **non-empty** stacks.
- At most `3 * 104` calls will be made to `push`, `pop`, `top`, and `getMin`.

```java
class MinStack {

    Node node;

    public MinStack() {
        node = new Node(Integer.MAX_VALUE, null, null, Integer.MAX_VALUE);
    }
    
    public void push(int val) {
        node.next = new Node(val, null, node, Math.min(val, node.min));
        node = node.next;
    }
    
    public void pop() {
        node = node.preNode;
        node.next = null;
    }
    
    public int top() {
        return node.val;
    }
    
    public int getMin() {
        return node.min;
    }
}

class Node{
    int val;
    int min;// 存一開始到當前最小
    Node preNode;
    Node next;

    Node(int val, Node next, Node preNode, int min) {
        this.val = val;
        this.next = next;
        this.preNode = preNode;
        this.min = min;
    }
}
/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(val);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```