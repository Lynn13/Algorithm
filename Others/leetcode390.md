### Elimination Game
- 这题目解法肯定很多，最简单的就是用几个标志位来表明进度
- head 当前队列的首个元素
- step 当前队列的元素之间的距离
- remaining 当前队列的元素个数
- left 当前是从左向右的操作

```
example:
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24
head = 1, left = true, step = 1, remaining = n(24)

完成第一次操作后：
2 4 6 8 10 12 14 16 18 20 22 24
head = 2, left = false, step = 1 * 2 = 2, remaining = remaining / 2 = 12

第二次操作，从右向左，要是现在是奇数个，那head就被除去了，要是偶数个，head就不动
2 4 6 8 10 12 14 16 18 20 22 24 - > 2 6 10 14 18 22
head = 2, left = true, step = 2 * 2 = 4, remaining = remaining / 2 = 6


2 6 10 14 18 22 - > 6 14 22
head = 6, left = false, step = 4 * 2 = 8, remaining = remaining / 2 = 3


6 14 22 - > 14
head = 14, left = true, step = 8 * 2 = 16, remaining = remaining / 2 = 1


```
