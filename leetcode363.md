## 363. Max Sum of Rectangle No Larger Than K
- 双层遍历行或列,形成一个区间
- 在这个区间中，相当于寻找一维数组中不超过K的最大的连续子序列
- 新建TREESET，记录每个连续子序列的值，
- 遍历过程中发现，如果`sum[j] - K`在TREESET中存在，那么就是一个可能的结果
- 和记录的最佳结果比较，得出最佳即可

- 复杂度`O(n^2  * mlogm)`，所以行和列谁在外循环谁就决定复杂度大不大，so可以比较出较小的一个放在外循环
```
import java.util.TreeSet;

class Solution {
    public int maxSumSubmatrix(int[][] matrix, int target) {
        int row = matrix.length;
        if (row == 0)
            return 0;

        int col = matrix[0].length;
        int m = Math.min(row,col);
        int n = Math.max(row,col);

        boolean colIsBig = col > row;
        int res = Integer.MIN_VALUE;

        for (int i = 0; i < m; i++){
            int[] a = new int[n];

            for (int j = i; j >= 0; j--){
                int curSum = 0;
                TreeSet<Integer> set = new TreeSet<>();
                set.add(0);

                for (int k = 0; k < n; k++){
                    a[k] += colIsBig ? matrix[j][k] : matrix[k][j];
                    curSum += a[k];
                    Integer start = set.ceiling(curSum - target);
                    if (start != null)
                        res = Math.max(res, curSum - start);
                    set.add(curSum);
                }
            }
        }

        return res;
    }
}
```
