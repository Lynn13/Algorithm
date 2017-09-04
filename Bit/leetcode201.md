# Bitwise AND of Numbers Range
- leetcode 201
- 题意： 给定一个区间，找出该区间所有元素“与”之后的结果。
- 递归的求解结果。如果m＝＝n，那么结果就是n，如果n>m，那么它们的最低位肯定是0，此时只需去计算n/2与m/2的结果，然后将结果左移一位。

```
class Solution {
    public int rangeBitwiseAnd(int m, int n) {
        if (m == n)
            return m;
        else 
            return rangeBitwiseAnd(m >> 1, n >> 1) << 1;
    }
}
```
