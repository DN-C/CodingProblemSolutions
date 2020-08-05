## Description

请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

## Thinking

（不考虑使用Java的replace）

1. 新开一个字符串，然后在原字符串上从前往后扫描，逐一复制，在遇到空格的时候原字符串进1，新字符串填入%20
2. 在原字符串的基础上，首先扫描一次，统计有多少个空格，然后进行扩容。扩容完成后，一个指针（或一个记录index的int）指向扩容完成的字符串末尾，一个指针指向原字符串的末尾，然后从后往前进行复制。遇到空格的时候第一个指针往前移动三次，并填入%20，第二个指针往前移动一次，最终当两个指针会和的时候，结束复制。



## Solutions





## Further

[StringBuffer class in Java](https://www.geeksforgeeks.org/stringbuffer-class-in-java/)