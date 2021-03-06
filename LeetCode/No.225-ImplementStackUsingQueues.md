## Description

Implement a last in first out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal queue (`push`, `top`, `pop`, and `empty`).

Implement the `MyStack` class:

- `void push(int x)` Pushes element x to the top of the stack.
- `int pop()` Removes the element on the top of the stack and returns it.
- `int top()` Returns the element on the top of the stack.
- `boolean empty()` Returns `true` if the stack is empty, `false` otherwise.

**Notes:**

- You must use **only** standard operations of a queue, which means only `push to back`, `peek/pop from front`, `size`, and `is empty` operations are valid.
- Depending on your language, the queue may not be supported natively. You may simulate a queue using a list or deque (double-ended queue), as long as you use only a queue's standard operations.

 

**Example 1:**

```
Input
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 2, 2, false]

Explanation
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top(); // return 2
myStack.pop(); // return 2
myStack.empty(); // return False
```

 

**Constraints:**

- `1 <= x <= 9`
- At most `100` calls will be made to `push`, `pop`, `top`, and `empty`.
- All the calls to `pop` and `top` are valid.

 

**Follow-up:** Can you implement the stack such that each operation is **[amortized](https://en.wikipedia.org/wiki/Amortized_analysis)** `O(1)` time complexity? In other words, performing `n` operations will take overall `O(n)` time even if one of those operations may take longer. You can use more than two queues.

## Thinking

pop() and top() are O(n), others are O(1).

There is another solution, which only push() is O(n), others are O(1).Go check link below.

## Solutions

~~~java
class MyStack {
    
    private Queue<Integer> queue;

    /** Initialize your data structure here. */
    public MyStack() {
        queue = new LinkedList<Integer>();
    }
    
    /** Push element x onto stack. */
    public void push(int x) {
        queue.offer(x);
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        int size = queue.size();
        for(int i = 0; i < size - 1; i++) {
            queue.offer(queue.poll());
        }
        return queue.poll();
    }
    
    /** Get the top element. */
    public int top() {
        int topE = this.pop();
        queue.offer(topE);
        return topE;
    
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return queue.peek() == null;
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
~~~



## Further

https://leetcode.com/problems/implement-stack-using-queues/discuss/62519/Only-push-is-O(n)-others-are-O(1).-Using-one-queue.-Combination-of-two-shared-solutions

https://leetcode.com/problems/implement-stack-using-queues/discuss/62519/Only-push-is-O(n)-others-are-O(1).-Using-one-queue.-Combination-of-two-shared-solutions