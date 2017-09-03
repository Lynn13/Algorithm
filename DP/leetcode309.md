# Best Time to Buy and Sell Stock with Cooldown

- leetcode 309

- 题意： 给定一个数组，代表了n天的股价。你可以交易任意多次，但是不允许交易之间相交，即上次的买必须卖出之后才允许再去买入。不过加了个条件，卖完之后必须是要休息一天。

- `The series of problems are typical dp`

- `buy[i]`在第i 天以buy结束的最大收益

- `sell[i]`在第i 天以sell结束的最大收益

- `rest[i]`在第i 天以rest结束的最大收益

- 状态转移公式

  ```
  price是第 i 天的价格
  buy[i]  = max(rest[i-1]-price, buy[i-1])  （i-1天买，第i天不能再买，只能休息）
  sell[i] = max(buy[i-1]+price, sell[i-1])  （i-1天卖，第i天只能休息）
  rest[i] = max(sell[i-1], buy[i-1], rest[i-1])
  ```

- 因为`buy[i] <= rest[i] <= sell[i]`,最后一天休息总比最后一天买的收益更高，最后一天卖出的收益总大于等于最后一条休息的收益

  ```
  rest[i] = sell[i-1]
  ```

- 化简为

  ```
  buy[i] = max(sell[i-2]-price, buy[i-1])
  sell[i] = max(buy[i-1]+price, sell[i-1])
  ```

- 代码

  ```
  class Solution {
      public int maxProfit(int[] prices) {
      if (prices.length == 0)
          return 0;
      if (prices.length == 1)
          return 0;
      int[] profitOfBuyy = new int[prices.length];
      int[] profitOfSell = new int[prices.length];
      profitOfBuyy[0] = -prices[0];
      profitOfBuyy[1] = Math.max(-prices[1], -prices[0]);
      profitOfSell[0] = 0;
      profitOfSell[1] = Math.max(prices[1] - prices[0], 0);
      for (int i = 2; i < prices.length; i++){
          profitOfBuyy[i] = Math.max(profitOfBuyy[i-1], profitOfSell[i-2] - prices[i]);
          profitOfSell[i] = Math.max(profitOfBuyy[i-1] + prices[i], profitOfSell[i-1]);
      }
      return profitOfSell[prices.length-1];
      }
  }
  ```

- 只用到了i i-1 i-2，可进行空间复杂度的化简

  ```
  public int maxProfit(int[] prices) {
  int sell = 0, prev_sell = 0, buy = Integer.MIN_VALUE, prev_buy;
  for (int price : prices) {
      prev_buy = buy;
      buy = Math.max(prev_sell - price, prev_buy);
      prev_sell = sell;
      sell = Math.max(prev_buy + price, prev_sell);
  }
  return sell;
  }
  ```

