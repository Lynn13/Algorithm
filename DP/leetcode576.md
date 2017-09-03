# Out of Boundary Paths

- leetcode 576

- 初始化`count[i][j] = 1`，这是`step = 0`的情况

- 循环step次，每次初始化一个新的`temp[i][j]`，分别以所有的点为起点运动一步，更新`temp[x][y] = (temp[x][y] + count[i][j]) % MOD`，如果越界，更新result

- 更新遍历完毕后，`count = temp`就完成了一次运动

  ```
  class Solution {
  public int findPaths(int m, int n, int N, int i, int j) {
      if (N < 0)
          return 0;
      int MOD = 1000000007;
      int[][] dirs = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
      int[][] count = new int[m][n];
      count[i][j] = 1;
      int result = 0;
  ```

```
    for (int step = 0; step < N; step++){
        int[][] temp = new int[m][n];
        for (int r = 0; r < m; r++){
            for (int c = 0; c < n; c++){
                for (int[] d : dirs){
                    int x = r + d[0];
                    int y = c + d[1];
                    if (x < 0 || x >= m || y < 0 || y >= n)
                        result = (result + count[r][c]) % MOD;
                    else
                        temp[x][y] = (temp[x][y] + count[r][c]) % MOD;
                }
            }
        }
        count = temp;
    }
    return result;
}
}
​```
```



