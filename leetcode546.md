- `d[i,j,k]`:区间`[i,j]`内，并且j段之后还有k个颜色和第j相同的方块，能得到的最大得分

### DFS DP

```
class Solution {
    public int removeBoxes(int[] boxes) {
        return dfS(boxes, new int[100][100][100], 0, boxes.length - 1, 0);
    }

    private int dfS(int[] boxes, int[][][] dp, int start, int end, int k){
        if (start > end)
            return 0;
        if (dp[start][end][k] != 0)
            return dp[start][end][k];

        //仅仅初始化一下，计算并不科学
        while (end > start && boxes[end] == boxes[end -1]){
            k++;
            end--;
        }
        dp[start][end][k] = dfS(boxes, dp, start, end - 1, 0) + (k + 1) * (k + 1);

        //DFS
        for (int i = start; i < end; i++){
            if (boxes[i] == boxes[end]){
                dp[start][end][k] = Math.max(dp[start][end][k], dfS(boxes, dp, start, i, k + 1) + dfS(boxes, dp, i+1, end, 0));
            }
        }

        return dp[start][end][k];
    }
}
```
