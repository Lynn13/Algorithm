# Partition Equal Subset Sum

- leetcode 416
- 实际上是个01背包问题，从所有的number中挑选，加和是所有和的1/2
- `dp[i][j] == true`表示：从0到 i 挑选的数的和可以是 j
- ` For each number, if we don't pick it, dp[i][j] = dp[i-1][j]`
- ` If we pick nums[i]. dp[i][j] = dp[i-1][j-nums[i]]`
- 这两种方法只需满足一个，`Thus, the transition function is dp[i][j] = dp[i-1][j] || dp[i-1][j-nums[i]]`
- 代码

```
public boolean canPartition(int[] nums) {
    int sum = 0;
    
    for (int num : nums) {
        sum += num;
    }
    
    if ((sum & 1) == 1) {
        return false;
    }
    sum /= 2;

    int n = nums.length;
    boolean[][] dp = new boolean[n+1][sum+1];
    for (int i = 0; i < dp.length; i++) {
        Arrays.fill(dp[i], false);
    }
    
    dp[0][0] = true;
    
    for (int i = 1; i < n+1; i++) {
        dp[i][0] = true;
    }
    for (int j = 1; j < sum+1; j++) {
        dp[0][j] = false;
    }
    
    for (int i = 1; i < n+1; i++) {
        for (int j = 1; j < sum+1; j++) {
            dp[i][j] = dp[i-1][j];
            if (j >= nums[i-1]) {
                dp[i][j] = (dp[i][j] || dp[i-1][j-nums[i-1]]);
            }
        }
    }
   
    return dp[n][sum];
}
```

