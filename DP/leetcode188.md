# Best Time to Buy and Sell Stock IV
- `dp[i][j]` 代表从0到j交易i次的结果
- `dp[k][len - 1]` 即最后结果
- 初始化`dp[i][0] = 0`
- 如果到j为止，pftBuy是买了第i个股票后的最优的收益，那么完成i个交易的最优的收益是`pftBuy + prices[j]`，也即
- `dp[i][j] = Math.max(dp[i][j-1], pftBuy + prices[j])`

```
class Solution {
    public int maxProfit(int k, int[] prices) {
        if(prices.length < 2){
            return 0;
        }
        if (k > prices.length / 2)
            return func(prices);

        int[][] dp = new int[k + 1][prices.length];
        dp[0][0] = 0;

        for (int i = 1; i <= k; i++){
            int pftBuy = dp[i - 1][0] - prices[0];
            for (int j = 1; j <= prices.length - 1; j++){
                pftBuy = Math.max(pftBuy, dp[i - 1][j - 1] - prices[j]);
                dp[i][j] = Math.max(dp[i][j-1], pftBuy + prices[j]);
                
            }
        }

        return dp[k][prices.length - 1];
    }

    private int func(int[] prices) {
        int len = prices.length, profit = 0;
        for (int i = 1; i < len; i++)
            // as long as there is a price gap, we gain a profit.
            if (prices[i] > prices[i - 1]) profit += prices[i] - prices[i - 1];
        return profit;
    }
}
```
