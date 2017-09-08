# Pacific Atlantic Water Flow
- `boolean[][] pacific` 表示这个点的水能不能流到p洋
- `boolean[][] atlanti` 表示这个点的水能不能流到a洋
- `pQueue`表示下一次要检测的点，检测时，上下左右移动，移动后的高度比当前高度高，那么这个点的水会流到p洋
- a洋同理

```

class Solution {
    public List<int[]> pacificAtlantic(int[][] matrix) {
        List<int[]> res = new ArrayList<>();
        if (matrix.length == 0)
            return res;

        boolean[][] pacific = new boolean[matrix.length][matrix[0].length];
        boolean[][] atlanti = new boolean[matrix.length][matrix[0].length];
        Queue<int[]> pQueue = new LinkedList<>();
        Queue<int[]> aQueue = new LinkedList<>();

        //初始化
        for (int i = 0; i < matrix.length; i++){
            pQueue.offer(new int[]{i, 0});
            pacific[i][0] = true;
            aQueue.offer(new int[]{i, matrix[0].length - 1});
            atlanti[i][matrix[0].length - 1] = true;
        }
        for (int i = 0; i < matrix[0].length; i++){
            pQueue.offer(new int[]{0, i});
            pacific[0][i] = true;
            aQueue.offer(new int[]{matrix.length - 1, i});
            atlanti[matrix.length - 1][i] = true;
        }

        //广搜遍历
        bfs(matrix, pQueue, pacific);
        bfs(matrix, aQueue, atlanti);

        //result
        for (int i = 0; i < matrix.length; i++){
            for (int j = 0; j < matrix[0].length; j++){
                if (pacific[i][j] && atlanti[i][j])
                    res.add(new int[]{i,j});
            }
        }

        return res;
    }

    void bfs(int[][]matrix, Queue<int[]> queue, boolean[][]visited){
        int[][] dir = new int[][]{{1,0},{-1,0},{0,1},{0,-1}};
        while (!queue.isEmpty()){
            int[] pos = queue.poll();
            for (int[] d : dir){
                int newI = pos[0] + d[0];
                int newJ = pos[1] + d[1];
                if (newI < 0 || newI >= matrix.length || newJ < 0 || newJ >= matrix[0].length)
                    continue;
                if (matrix[newI][newJ] < matrix[pos[0]][pos[1]])
                    continue;
                if (visited[newI][newJ])
                    continue;
                visited[newI][newJ] = true;
                queue.offer(new int[]{newI, newJ});
            }
        }
    }
}
```
