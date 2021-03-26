## Description

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

 

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

- `-231 <= val <= 231 - 1`
- Methods `pop`, `top` and `getMin` operations will always be called on **non-empty** stacks.
- At most `3 * 104` calls will be made to `push`, `pop`, `top`, and `getMin`.

## Thinking



## Solutions

~~~java
class MinStack {
    Stack<Long> s;
    Long min;

    /** initialize your data structure here. */
    public MinStack() {
        s = new Stack<Long>();
        min = 0L;
    }
    
    public void push(int val) {
        if(s.empty()) {
            s.push(0L);
            min = (long)val;
        } else {
            s.push((long)(val - min));
            if(val < min) min = (long)val;
        }
    }
    
    public void pop() {
        if(s.empty()) return;
        Long p = s.pop();
        if(p < 0) min = min - p;
    }
    
    public int top() {
        Long top = s.peek();
        if(top > 0) return (int)(top + min);
        else return (int)(min + 0);
    }
    
    public int getMin() {
        return (int)(min + 0);
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
~~~



## Further

https://leetcode.com/problems/min-stack/discuss/49031/Share-my-Java-solution-with-ONLY-ONE-stack

https://leetcode.com/problems/min-stack/discuss/49010/Clean-6ms-Java-solution