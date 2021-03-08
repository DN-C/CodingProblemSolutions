## Description

Count the number of prime numbers less than a non-negative number, `n`.

 

**Example 1:**

```
Input: n = 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
```

**Example 2:**

```
Input: n = 0
Output: 0
```

**Example 3:**

```
Input: n = 1
Output: 0
```

 

**Constraints:**

- `0 <= n <= 5 * 106`

## Thinking

Go Google *Sieve of Eratosthenes*.

## Solutions

~~~java
class Solution {
    public int countPrimes(int n) {
        if(n < 2) return 0;
        boolean notPrime[] = new boolean[n];
        for(int i = 2; i * i < n; ++i) {
            if(!notPrime[i]) {
                for(int j = i * i; j < n; j += i) {
                    notPrime[j] = true;
                }
            }
        }
        int res = 0;
        for(int i = 2; i < n; ++i) {
            if(!notPrime[i]) ++res;
        }
        return res;
    }
}
~~~



## Further

https://github.com/labuladong/fucking-algorithm/blob/master/%E9%AB%98%E9%A2%91%E9%9D%A2%E8%AF%95%E7%B3%BB%E5%88%97/%E6%89%93%E5%8D%B0%E7%B4%A0%E6%95%B0.md