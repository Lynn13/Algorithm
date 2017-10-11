## 给出两个字符串，最少需要多少步能让word1转变成word2？
- DP
- `DP[i][j]`表示word1[0...i-1]转变成word2[0...j-1]的步骤
- 初始`dp[i][0] = i  dp[0][j] = j`
- let's consider `word[i - 1] and word2[j - 1]`. If they are euqal, then no more operation is needed and `dp[i][j] = dp[i - 1][j - 1]`. 
- if they are not equal,
- Replace word1[i - 1] by word2[j - 1] (dp[i][j] = dp[i - 1][j - 1] + 1
- Delete word1[i - 1] and word1[0..i - 2] = word2[0..j - 1] (dp[i][j] = dp[i - 1][j] + 1 
- Insert word2[j - 1] to word1[0..i - 1] and word1[0..i - 1] + word2[j - 1] = word2[0..j - 1] (dp[i][j] = dp[i][j - 1] + 1
- 下面代码是可以优化空间的

```
class Solution {
    public int minDistance(String word1, String word2) {
        int[][] dp = new int[word1.length()+1][word2.length()+1];
        for(int i = 1; i <= word1.length(); i++){
            dp[i][0] = i;
        }
        for(int j = 1; j <= word2.length(); j++){
            dp[0][j] = j;
        }

        for(int i = 1; i <= word1.length(); i++){
            for(int j = 1; j <= word2.length(); j++){
                if(word1.charAt(i-1) == word2.charAt(j-1)){
                    dp[i][j] = dp[i - 1][j - 1];
                }
                else{
                    dp[i][j] = Math.min(dp[i-1][j-1] + 1, Math.min(dp[i][j-1] + 1, dp[i - 1][j] + 1));
                }
            }
        }

        return dp[word1.length()][word2.length()];
    }
}
```
