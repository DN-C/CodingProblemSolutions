## Description

Implement `FreqStack`, a class which simulates the operation of a stack-like data structure.

`FreqStack` has two functions:

- `push(int x)`, which pushes an integer `x` onto the stack.

- ```
  pop()
  ```

  , which

   

  removes

   

  and returns the most frequent element in the stack.

  - If there is a tie for most frequent element, the element closest to the top of the stack is removed and returned.

 

**Example 1:**

```
Input: 
["FreqStack","push","push","push","push","push","push","pop","pop","pop","pop"],
[[],[5],[7],[5],[7],[4],[5],[],[],[],[]]
Output: [null,null,null,null,null,null,null,5,7,5,4]
Explanation:
After making six .push operations, the stack is [5,7,5,7,4,5] from bottom to top.  Then:

pop() -> returns 5, as 5 is the most frequent.
The stack becomes [5,7,5,7,4].

pop() -> returns 7, as 5 and 7 is the most frequent, but 7 is closest to the top.
The stack becomes [5,7,5,4].

pop() -> returns 5.
The stack becomes [5,7,4].

pop() -> returns 4.
The stack becomes [5,7].
```

 

**Note:**

- Calls to `FreqStack.push(int x)` will be such that `0 <= x <= 10^9`.
- It is guaranteed that `FreqStack.pop()` won't be called if the stack has zero elements.
- The total number of `FreqStack.push` calls will not exceed `10000` in a single test case.
- The total number of `FreqStack.pop` calls will not exceed `10000` in a single test case.
- The total number of `FreqStack.push` and `FreqStack.pop` calls will not exceed `150000` across all test cases.

## Thinking

Fully credited to @Lee215

Use an integer-to-stack map to store characters in different frequency. For example, 1 is pushed 3 times, than 1 store in stack1, 2 and 3. 

Every time pop, pop the stack store the most frequently elements. This will guarantee that most frequent element, which when there are many options, the closest to the top of the stack one,  will be popped. When the stack represent one frequency is empty, remove it from the map.

## Solutions

~~~java
class FreqStack {
    Map<Integer, Integer> freq;
    Map<Integer, Stack<Integer>> map;

    public FreqStack() {
        freq = new HashMap<Integer, Integer>();
        map = new HashMap<Integer, Stack<Integer>>();
    }
    
    public void push(int x) {
        int f = freq.getOrDefault(x, 0) + 1;
        freq.put(x, f);
        if(!map.containsKey(f)) map.put(f, new Stack<Integer>());
        map.get(f).push(x);
    }
    
    public int pop() {
        int maxFreq = map.size();
        int res = map.get(maxFreq).pop();
        freq.put(res, freq.get(res) - 1);
        if(map.get(maxFreq).size() == 0) map.remove(maxFreq);
        return res;
    }
}

/**
 * Your FreqStack object will be instantiated and called as such:
 * FreqStack obj = new FreqStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 */
~~~



## Further

Genius Lee215: https://leetcode.com/problems/maximum-frequency-stack/discuss/163410/C%2B%2BJavaPython-O(1)