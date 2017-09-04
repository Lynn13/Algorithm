# Single Number II
- leetcode 137
#### 解法1
- 这种解法同样适用于leetcode136以及所有同类问题，但不如解法2吊。
- 每一位上出现要么为1 ，要么为0。对数组，统计每一位上1 出现的次数count，必定是3N或者3N+1 次。让count对3取模，能够获得到那个只出现1次的元素该位是0还是1。

#### 解法2
- 对3取余有3种状态，00/01/10
- 对结果的每一位用两个bit来表示这一位计算的结果
- 例子：
- 输入：1100,1100,1100,1001，结果是1001
- 处理1100，得到01-01-00-00
- 处理1100，得到10-10-00-00
- 处理1100，得到00-00-00-00
- 处理1001，得到01-00-00-01
- 得结果1001

```
two |= one & nums[i] 
one ^= nums[i]       #新来的为0，one不变，新来为1时，one是0、1交替改变
three = one & two    #当one和two为1是，three为1（此时代表要把one和two清零了）
one &= ~three        #把one清0
two &= ~three        #把two清0

```

```
public int singleNumber(int[] A) {
    int ones = 0, twos = 0;
    for(int i = 0; i < A.length; i++){
        ones = (ones ^ A[i]) & ~twos;
        twos = (twos ^ A[i]) & ~ones;
    }
    return ones;
}
```
