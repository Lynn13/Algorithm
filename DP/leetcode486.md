# Predict the Winner

- leetcode 486
- `dp[i][j]`表示从`num[i]` 到 `num[j]`，第一个人比第二个人能多获得多少分
- 基本状态是 `dp[i][i] = nums[i]`
- 如果第一个人选`num[i]`,那么`dp[i][j] = nums[i] - dp[i + 1][j]`
- 如果第一个人选`num[j]`,那么`dp[i][j] = nums[j] - dp[i][j - 1]`
- 即`dp[i][j] = Math.max(nums[i] - dp[i + 1][j], nums[j] - dp[i][j - 1]);`

```
class Solution {
    public boolean PredictTheWinner(int[] nums) {
        if (nums.length == 0)
            return false;
        int[][] dp = new int[nums.length][nums.length];
        for (int i = 0; i < nums.length; i++)
            dp[i][i] = nums[i];

        for (int len = 1; len < nums.length; len++){
            for (int i = 0; i + len < nums.length; i++){
                int j = i + len;
                dp[i][j] = Math.max(nums[i] - dp[i + 1][j], nums[j] - dp[i][j - 1]);
            }
        }
        return dp[0][nums.length-1] >= 0;
    }
}
```

# 