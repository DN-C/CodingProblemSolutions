## Description



## Thinking



## Solutions

~~~java
//Solution 1
class Solution {
    public int numberOfArithmeticSlices(int[] A) {
        int len = A.length;
        if(len < 3) return 0;
        int preNum = A[1], diff = A[1] - A[0], lenOfSlice = 2, res = 0;
        for(int i = 2; i < len; i++) {
            if(A[i] - preNum == diff) {
                ++lenOfSlice;
                if(lenOfSlice > 2) res += (lenOfSlice - 2);
                preNum = A[i];
            System.out.println(lenOfSlice);
            } else {
                diff = A[i] - preNum;
                preNum = A[i];
                lenOfSlice = 2;
            }
        }
        return res;
    }
}

//Solution 2. Basically the better one ccomparing to solution 1, refference(go check Further part) by @lcl7722
class Solution {
    public int numberOfArithmeticSlices(int[] A) {
        int len = A.length;
        if(len < 3) return 0;
        int cur = 0, res = 0;
        for(int i = 2; i < len; i++) {
            if(A[i] - A[i - 1] == A[i - 1] - A[i - 2]) {
                res += ++cur;
            } else {
                cur = 0;
            }
        }
        return res;
    }
}
~~~



## Further

https://leetcode.com/problems/arithmetic-slices/discuss/90058/Simple-Java-solution-9-lines-2ms