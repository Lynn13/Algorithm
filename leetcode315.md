### 解法1：构建二分搜索树
- 把NODE的结构设置为：
    ```
    class Node{
        Node left;
        Node right;
        int val;
        int count;//有多少个比本node小的node
        int dup;  //有多少个相同值的node
        public Node(int v, int s){
            val = v;
            count = s;
            dup = 1;
        }
    }
    ```
- 从第length-1到第0个依次进行插入，每次插入是一个DFS
- 插入的值和本node值相同：dup++
- 插入的值 > 本node值：遍历右子树
- 插入的值 < 本node值：count++ 遍历左子树
```
import java.lang.reflect.Array;
import java.util.Arrays;
import java.util.List;

class Solution {
    class Node{
        Node left;
        Node right;
        int val;
        int count;
        int dup;
        public Node(int v, int s){
            val = v;
            count = s;
            dup = 1;
        }
    }

    public List<Integer> countSmaller(int[] nums) {
        Integer[] res = new Integer[nums.length];
        Node root = null;
        for (int i = nums.length - 1; i >= 0; i--){
            root = insert(nums[i], root, res, i, 0);
        }
        return Arrays.asList(res);
    }

    private Node insert(int num, Node node, Integer[] res, int i, int preCount){
        if (node == null){
            node = new Node(num, 0);
            res[i] = preCount;
        }
        else if (node.val == num){
            node.dup++;
            res[i] = preCount + node.count;
        }
        else if (node.val > num){
            node.count++;
            node.left = insert(num, node.left, res, i, preCount);
        }
        else {
            node.right = insert(num, node.right, res, i, preCount + node.count + node.dup);
        }
        return node;
    }
}

```

### 解法2：合并排序
- 对于某个特定的数据，其后面的逆序数等于在排序过程中需要移动到该数前面的个数
- 过程中，用pos[]保存每个数字的原始index，用smaller[]保存每个数字后面比自己小的数量
- 其他和一般的合并排序一样

```
import java.lang.reflect.Array;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {


    public List<Integer> countSmaller(int[] nums) {
        int[] smaller = new int[nums.length];
        int[] pos = new int[nums.length];
        for (int i = 0; i < pos.length; i++){
            pos[i] = i;
        }

        sort(nums, pos, smaller, 0, nums.length - 1);
        List<Integer> res = new ArrayList<>();
        for (int i = 0 ; i < smaller.length; i++){
            res.add(smaller[i]);
        }
        return res;
    }

    private void sort(int[] nums, int[] pos, int[] smaller, int from, int to){
        if (from >= to)
            return;
        int mid= (from + to) / 2;
        sort(nums, pos, smaller, from, mid);
        sort(nums, pos, smaller, mid + 1, to);

        int[] merge = new int[to - from + 1];
        int i = from;
        int j = mid + 1;
        int k = 0;
        int jump = 0;

        while (i <= mid && j <= to){
            if (nums[pos[i]] <= nums[pos[j]]){
                merge[k] = pos[i];
                smaller[pos[i]] += jump;
                i++;
            }
            else {
                merge[k] = pos[j];
                jump++;
                j++;
            }
            k++;
        }

        while (i <= mid){
            merge[k] = pos[i];
            smaller[pos[i]] += jump;
            i++;
            k++;
        }

        while (j <= to){
            merge[k] = pos[j];
            j++;
            k++;
        }

        for (int i2 = from; i2 < to; i2++){
            pos[i2] = merge[i2 - from];
        }
    }

}

```

