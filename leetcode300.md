### Longest Increasing Subsequence
### O(n2)
- `dp[i]`表示以i位置结束的最长子序列的长度
```
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
    if (nums.size() == 0) return 0;
        vector<int> dp(nums.size(), 1);
        int res = 1;
        for (int i = 1; i < nums.size(); ++i){
                        // 每次外部循环，确定以当前位置为末尾元素的最长子序列；
            for (int j = 0; j < i; ++j){
                if (nums[j] < nums[i]){
                    dp[i] = max(dp[i], 1+dp[j]);
                                // 通过遍历 j 实现对 dp[i] 的更新
                }
            }
            res = max(res, dp[i]);
        }
        return res;
    }
};
```


### O(nlogn)
- 先建立一个数组ends，放入nums的首元素
- 如果遍历到的新元素比ends数组中的首元素小的话，替换首元素为此新元素，
- 如果遍历到的新元素比ends数组中的末尾元素还大的话，将此新元素添加到ends数组末尾(注意不覆盖原末尾元素)。
- 如果遍历到的新元素比ends数组首元素大，比尾元素小时，此时用二分查找法找到第一个不小于此新元素的位置，覆盖掉位置的原来的数字
- 以此类推直至遍历完整个 nums 数组，此时 ends 数组的长度就是我们要求的 LIS 的长度
- 【特别注意的是】 ends 数组的值可能不是一个真实的LIS，比如若输入数组nums为 {4, 2， 4， 5， 3， 7}，那么算完后的ends数组为{2， 3， 5， 7}，可以发现它不是一个原数组的LIS，只是长度相等而已，千万要注意这点

### 上述解法的优化版
```
public int lengthOfLIS(int[] nums) {
    int[] tails = new int[nums.length];
    int size = 0;
    for (int x : nums) {
        int i = 0, j = size;
        while (i != j) {
            int m = (i + j) / 2;
            if (tails[m] < x)
                i = m + 1;
            else
                j = m;
        }
        tails[i] = x;
        if (i == size) ++size;
    }
    return size;
}
```
