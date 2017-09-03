## Maximal Square
- `A[i][j]`表示的就是以(i,j)为右下角的最大的正方形的边长
- `A[i][j] = min(A[i-1][j-1], A[i-1][j], A[i][j-1]) + 1`
- ![image](https://github.com/Lynn13/Algorithm/blob/master/DP/image/leetcode221.png)

```
class Solution {
    public int maximalSquare(char[][] matrix) {
        if (matrix.length == 0)
            return 0;
        
        int result = 0;
        int[][] dp = new int[matrix.length][matrix[0].length];

        for (int i = 0; i < matrix.length; i++){
            for (int j = 0; j < matrix[0].length; j++){
                if (matrix[i][j] == '1'){
                    dp[i][j] = 1;
                    if (i > 0 && j > 0){
                        dp[i][j] = 1 + Math.min(Math.min(dp[i - 1][j], dp[i][j - 1]), dp[i - 1][j - 1]);
                    }
                    result = Math.max(result, dp[i][j]);
                }
            }
        }

        return result * result;
    }
}
```
