 ## Description

在一个长度为n的数组里的所有数字都在0到n-1的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。 例如，如果输入长度为7的数组{2,3,1,0,2,5,3}，那么对应的输出是第一个重复的数字2。



## Thinking

1. 数组排序（快排）后，检查数字与序号是否相等，不相等则说明该数字为重复数字。时间复杂度 O(nlogn)。
2. 哈希表，时间复杂度 O(n) ，但需要一个 O(n) 的哈希表。
3. 遍历数组，将当前位置的数字与对应位置的数字进行比较，不同则交换，相同则说明为重复数字。



## Solution

### Sort

### Hash

~~~java
import java.util.HashMap;

public class Solution {
    // Parameters:
    //    numbers:     an array of integers
    //    length:      the length of array numbers
    //    duplication: (Output) the duplicated number in the array number,length of duplication array is 1,so using duplication[0] = ? in implementation;
    //                  Here duplication like pointor in C/C++, duplication[0] equal *duplication in C/C++
    //    这里要特别注意~返回任意重复的一个，赋值duplication[0]
    // Return value:       true if the input is valid, and there are some duplications in the array number
    //                     otherwise false
    public boolean duplicate(int numbers[],int length,int [] duplication) {
        HashMap<Integer, Integer> check = new HashMap<Integer, Integer>();
        for (int i = 0; i < length; i++) {
            if (check.containsKey(numbers[i])) {
                duplication[0] = numbers[i];
                return true;
            } else {
                check.put(numbers[i], 1);
            }
        }
        
        return false;
    }
}
~~~



### Check and exchange

~~~java
public class Solution {
    // Parameters:
    //    numbers:     an array of integers
    //    length:      the length of array numbers
    //    duplication: (Output) the duplicated number in the array number,length of duplication array is 1,so using duplication[0] = ? in implementation;
    //                  Here duplication like pointor in C/C++, duplication[0] equal *duplication in C/C++
    //    这里要特别注意~返回任意重复的一个，赋值duplication[0]
    // Return value:       true if the input is valid, and there are some duplications in the array number
    //                     otherwise false
    public boolean duplicate(int numbers[],int length,int [] duplication) {
        for (int i = 0; i < length; i++) {
            while (numbers[i] != i) {
                int temp = numbers[i];
                if (temp >= length) {
                    return false;
                }
                if (temp == numbers[temp]) {
                    duplication[0] = temp;
                    return true;
                }
                numbers[i] = numbers[temp];
                numbers[temp] = temp;
            }
        }
        
        return false;
    }
}
~~~



## 

## Further

https://www.nowcoder.com/questionTerminal/623a5ac0ea5b4e5f95552655361ae0a8?f=discussion