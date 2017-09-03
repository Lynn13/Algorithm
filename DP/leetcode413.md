# Arithmetic Slices

- leetcode 413
- `dp[i]`表示以`A[i]`为结尾的序列
- 代码

```
class Solution {
    public int numberOfArithmeticSlices(int[] A) {
        if (A.length < 3)
            return 0;
        int[] dp = new int[A.length + 1];
        dp[0] = 0;
        dp[1] = 0;
        dp[2] = A[2] - A[1] == A[1] - A[0] ? 1 : 0;
        int result = dp[2];
        for (int i = 3; i < A.length; i++){
            if (A[i] - A[i - 1] == A[i - 1] - A[i - 2]){
                dp[i] = dp[i - 1] + 1;
                result += dp[i];
            }
            else {
                dp[i] = 0;
            }
        }
        return result;
    }
}
```

