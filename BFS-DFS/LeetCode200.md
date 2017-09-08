### Number of Islands
- 基本思路就是见到一个陆地，就把和它连接的所有陆地都变成海洋。

```
class Solution {
    public int numIslands(char[][] grid) {
        if (grid.length == 0)
            return 0;
        int res = 0;
        for (int i = 0; i < grid.length; i++){
            for (int j = 0; j < grid[0].length; j++){
                if (grid[i][j] == '1'){
                    dfs(grid, i, j);
                    res++;
                }
            }
        }

        return res;
    }

    public void dfs(char[][] grid, int i, int j){
        if (i < 0 || i >=grid.length || j < 0 ||j >= grid[0].length)
            return;
        if (grid[i][j] == '0')
            return;
        grid[i][j] = '0';
        dfs(grid, i - 1, j);
        dfs(grid, i, j - 1);
        dfs(grid, i + 1, j);
        dfs(grid, i, j + 1);
    }
}
```
