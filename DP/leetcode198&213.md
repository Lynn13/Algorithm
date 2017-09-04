# House Robber

- leetcode 198

- leetcode 213

- 都很简单，第i个抢，`dp[i][抢] = dp[i-1][不抢] + num[i]`,第i个不抢，`dp[i][不抢] = max(dp[i-1][不抢]，dp[i-1][抢])`，然后全程都是i和i-1，完全可以优化空间复杂度为o（1）

- 198代码


  ```
  public int rob(int[] num) {

  int prevNo = 0;

  int prevYes = 0;

  for (int n : num) {
 
      int temp = prevNo;

      prevNo = Math.max(prevNo, prevYes);

      prevYes = n + temp;
 
  }

  return Math.max(prevNo, prevYes);

  }
  ```

- 213只是把198的num环起来了，只要判断一下第一个抢不抢，就可以完全套用198的代码

- 213代码



  ```
  class Solution {

  public int rob(int[] nums) {
 
      if (nums.length == 1)

          return nums[0];

      return Math.max(rob(nums, 0, nums.length-2), rob(nums, 1, nums.length-1));
 
  }

  public int rob(int[] nums, int lo, int hi){

      int include = 0;
 
      int exclude = 0;
 
      for (int j = lo; j <= hi; j++){
 
          int lastInclude = include;
 
          int lastExclude = exclude;

          include = nums[j] + lastExclude;
 
          exclude = Math.max(lastInclude, lastExclude);
 
      }

      return Math.max(include, exclude);

  }

  }
  ```
