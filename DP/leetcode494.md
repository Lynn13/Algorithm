# Target Sum

- leetcode 494
- p 结果中的正数
- n 结果中的负数
- 简化：

```
sum(P) - sum(N) = target
sum(P) + sum(N) + sum(P) - sum(N) = target + sum(P) + sum(N)
2 * sum(P) = target + sum(nums)
```

- so，只需要从nums中找到一些数使和为allSum+S的1/2，具体参考leetcode 416
- `dp[j]`表示有多少种组合使和为`j`
- 假如`nums = {1,4,15,56}  target = 60`，那么`dp[60] = dp[60-56],dp[4] = dp[4-4],dp[0]=1`
- 代码

```
class Solution {
    public int findTargetSumWays(int[] nums, int S) {
        int allSum = 0;
        for (int i = 0; i < nums.length; i++){
            allSum += nums[i];
        }
        if ((allSum+S) % 2 == 1 || allSum < S)
            return 0;
        return fun(nums, (allSum+S)/2);
    }

    public int fun(int[] nums, int target){
        int[] dp = new int[target+1];
        dp[0] = 1;
        for (int n : nums){
            for (int j = target; j >= n; j--){
                dp[j] += dp[j - n];
            }
        }
        return dp[target];
    }
}
```

