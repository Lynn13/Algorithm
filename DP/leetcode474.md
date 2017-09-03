# Ones and Zeroes

- leetcode 474
- 01背包
- `dp[k][m][n]`表示前k个字符串中，0个数不超过m，1个数不超过n的情况下能取的字符串个数
- 如果第k 个字符串中，0个数为count0，1个数为count1
- 取第i个字符串则`dp[k]m][n] = dp[k-1][m-cnt0][n-cnt1] + 1`
- 不取第i个字符串则`dp[k][m][n] = dp[k-1][m][n]`
- 取两者较大的作为dp[i][j][k]的值
- 由于dp[i][j][k]只与dp[i-1][？][？]相关，所以这里可以重复使用m x n个数据将空间复杂度降为O(m x n)
- 代码

```
class Solution {
    public int findMaxForm(String[] strs, int m, int n) {
        int[][] dp = new int[m+1][n+1];
        for (String s : strs){
            int count0 = 0;
            int count1 = 0;
            for (int i = 0; i < s.length(); i++){
                if (s.charAt(i) == '0')
                    count0++;
                else
                    count1++;
            }

            for (int i = m; i >=count0; i-- ){
                for (int j = n; j >= count1; j--){
                    dp[i][j] = Math.max(dp[i][j], 1 + dp[i - count0][j - count1]);
                }
            }
        }
        return dp[m][n];
    }
}
```

