## Description

The **Fibonacci numbers**, commonly denoted `F(n)` form a sequence, called the **Fibonacci sequence**, such that each number is the sum of the two preceding ones, starting from `0` and `1`. That is,

```
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), for N > 1.
```

Given `N`, calculate `F(N)`.

 

**Example 1:**

```
Input: 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.
```

**Example 2:**

```
Input: 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.
```

**Example 3:**

```
Input: 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
```

 

**Note:**

0 ≤ `N` ≤ 30.

## Thinking

递归+备忘录orDP数组

## Solutions

~~~java
// Solution 1 recrusive + reminder / DP Topdown
class Solution {
    public int fib(int N) {
        int array[] = new int[31];
        return reminder(N, array);
    }
    
    public int reminder(int N, int[] array) {
        if (N <= 0) return 0;
        if (N == 1) return 1;
        if (array[N] != 0) return array[N];
        array[N] = reminder(N - 1, array) + reminder(N - 2, array);
        return array[N];
    }
}

//  DP Bottomup
class Solution {
    public int fib(int N) {
        int fibCache[] = new int[31];
        for(int i = 0; i <= N; i++) {
           if (i == 0) fibCache[i] = 0;
           else if (i == 1) fibCache[i] = 1;
           else {
               fibCache[i] = fibCache[i - 1] + fibCache[i - 2];
           }
        }
        return fibCache[N];
    }
    
}

// Solution DP bottom-up with space O(1)
class Solution {
    public int fib(int N) {
        int sum = 0;
        int beforeSum1 = 0;
        int beforeSum2 = 0;
        for(int i = 0; i <= N; i++) {
            if (i == 1) {
                sum += 1;   
                continue;
            }
            beforeSum2 = beforeSum1;
            beforeSum1 = sum;
            sum = beforeSum1 + beforeSum2;
        }
        return sum;
    }
    
}
~~~



## Further

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie/dong-tai-gui-hua-xiang-jie-jin-jie

https://leetcode.com/problems/fibonacci-number/discuss/215992/Java-Solutions