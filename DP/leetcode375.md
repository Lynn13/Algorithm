# Guess Number Higher or Lower II

- leetcode 375

- 这题`II`和`I`在解题思路上没一点关系，跟二分查找没有一点关系，忘记题`I`吧，我一开始陷入了“既然猜数肯定是二分查找，既然是二分查找，那猜的路线是一定的，怎么会有最好最坏的情况一说？”的误区。

- 问至少需要多少钱才保证绝对能猜中，也就是对于n，要找出猜的最差的情况

- 先想一个区域`[start,end]`,如果猜`i`,那么`temp = i + Math.max(dp(dp, start, i-1), dp(dp, i+1, end));`

- 只需要遍历此区域，就可以找出此区域花费最少的猜数路线

- 代码

  ```
  class Solution {
  public int getMoneyAmount(int n) {
      return dp(new int[n+1][n+1], 1, n);
  }

  public int dp(int[][] dp, int start, int end){
      int result = Integer.MAX_VALUE;
      if (start >= end)
          return 0;
      if (dp[start][end] != 0)
          return dp[start][end];
      for (int i = start; i <= end; i++){
          int temp = i + Math.max(dp(dp, start, i-1), dp(dp, i+1, end));
          result = Math.min(result, temp);
      }
      dp[start][end] = result;
      return result;
  }
  }
  ```

