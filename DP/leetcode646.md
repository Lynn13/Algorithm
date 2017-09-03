# Maximum Length of Pair Chain

- leetcode 646
- `dp[i]`表示以`pair[i]`为结尾的链
- 代码

```
class Solution {
    public int findLongestChain(int[][] pairs) {
        int[] dp = new int[pairs.length];
        Arrays.fill(dp, 1);
        Arrays.sort(pairs, new Comparator<int[]>() {
            @Override
            public int compare(int[] o1, int[] o2) {
                return o1[0] - o2[0];
            }
        });

        for (int i = 0; i < pairs.length; i++){
            for (int j = 0; j < i; j++){
                int tmp = pairs[i][0] > pairs[j][1] ? dp[j] + 1 : dp[i];
                dp[i] = Math.max(dp[i], tmp);
            }
        }
        return dp[pairs.length - 1];
    }
}
```

