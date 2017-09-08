### 二叉树的层级遍历（每层都分开）
- 一个queue
- 每次放进queue的都属于同一层
- 获取queue的元素数量，就能明确知道要进行几次以下操作
- 依次拿出当前一层queue的所有元素，把元素的值放进sublist，把元素的左右节点放进queue
- 当前层操作完，queue内都是下一层的了，把sublist放进结果，本层ok


```
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null)
            return result;

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()){
            int num = queue.size();
            List<Integer> list = new ArrayList<>();
            for (int i = 0; i < num; i++){
                TreeNode node = queue.poll();
                if (node.left != null)
                    queue.offer(node.left);
                if (node.right != null)
                    queue.offer(node.right);
                list.add(node.val);
            }
            result.add(list);
        }

        return result;
    }
}
```
