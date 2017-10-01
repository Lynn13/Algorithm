```
class Solution {
     /**
     * dp【i】【j】表示当前状态是key的第i个字符，并且ring的第j个字符处于最上方
     * dp[i][j] = Math.min(dp[i][j], step + dp[i+1][k]);
     * dp[i][j]值表示走了多少步，没什么实际意义
     * 从后往前遍历一遍，最后得出dp[0][0]的值，dp[0][0]也就是最初的状态
     */
    public int findRotateSteps(String ring, String key) {
        int[][] dp = new int[key.length() + 1][ring.length()];

        for (int i = key.length() - 1; i >= 0; i--){
            for (int j = ring.length()-1; j >= 0; j--){
                dp[i][j] = Integer.MAX_VALUE;
                for (int k = 0; k < ring.length(); k++){
                    if (key.charAt(i) == ring.charAt(k)){
                        int diff = Math.abs(j - k);
                        int step = Math.min(diff, ring.length() - diff);
                        dp[i][j] = Math.min(dp[i][j], step + dp[i+1][k]);
                    }
                }
            }
        }

        return dp[0][0] + key.length();
    }
}
```
