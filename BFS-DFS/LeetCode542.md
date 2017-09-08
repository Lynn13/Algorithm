### 01 Matrix
- 一个queue
- 遍历所有点，val=1的设为val=Integer.MAX, val=0的进queue
- 每次从queue中poll出一个点，进行以下操作，直到queue空
- 上下左右移动，移动后过界了就跳过；移动后的值<=移动前的值，跳过；
- 移动后的值 > 移动前的值，把移动后的点的值设置为（移动前的点的值+1）

```
class Solution {
    public int[][] updateMatrix(int[][] matrix) {
        Queue<int[]> queue = new LinkedList<>();
        for (int i = 0; i < matrix.length; i++){
            for (int j = 0; j < matrix[0].length; j++){
                if (matrix[i][j] == 0)
                    queue.offer(new int[]{i, j});
                else
                    matrix[i][j] = Integer.MAX_VALUE;
            }
        }

        int[][] dirs = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
        while (!queue.isEmpty()){
            int[] cell = queue.poll();
            for (int[] d : dirs){
                int r = cell[0] + d[0];
                int c = cell[1] + d[1];
                if (matrix[r][c] <= matrix[cell[0]][cell[1]])
                    continue;
                if (r < 0 || r >= matrix.length || c < 0 || c >= matrix[0].length)
                    continue;
                queue.offer(new int[]{r, c});
                matrix[r][c] = matrix[cell[0]][cell[1]] + 1;
            }
        }
        return matrix;
    }
}
```
