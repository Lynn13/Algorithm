### Distinct Subsequences
- `mem[i+1][j+1]`表示`T[0..i]`在`S[0..j]`的基础上有多少种方法（删除字符）得到
- 最后结果为 `mem[T.length()][S.length()]`
- 初始化：
- 空字符只有一种方法得到，因此`mem[0][j] = 1` for every j，包括`mem[0][0] = 1`
- `mem[1][0] 到 mem[i][0]`都是0
- 动态规划公式：
- `mem[i+1][j+1]`除了由`mem[i+1][j]`组成，在`T[i] == S[j]`时还由`mem[i][j]`组成

```
class Solution {
    public int numDistinct(String s, String t) {
        int[][] dp = new int[t.length() + 1][s.length() + 1];

        for (int i = 0; i <= s.length(); i++){
            dp[0][i] = 1;
        }

        for (int i = 0; i < t.length(); i++){
            for (int j = 0; j < s.length(); j++){
                if (t.charAt(i) == s.charAt(j)){
                    dp[i + 1][j + 1] = dp[i + 1][j] + dp[i][j];
                }
                else {
                    dp[i + 1][j + 1] = dp[i + 1][j];
                }
            }
        }

        return dp[t.length()][s.length()];
    }
}
```
