## Populating Next Right Pointers in Each Node
-  a perfect binary tree
- 一层层来，A节点的左节点连接右节点，A右节点连接A.next节点的左节点

## Populating Next Right Pointers in Each Node 2
- a any binary tree
- 也是一层层来，没有规律的二叉树，那就记录一下上一个节点（prevNode）和下一层的首节点（headNode）
- 当数到节点cur时，cur和cur.next一定是确定的
- 如果当前headNode和prevNode是空，那么就是刚刚进行这一层，cur.left或者cur.head一定是head，除非下一层没了
- 剩下的就是prev和cur的一顿瞎赋值
- 结束的条件就是，本层走完了，下一层的head还是null
```
/**
 * Definition for binary tree with next pointer.

 */
public class Solution {
    public void connect(TreeLinkNode root) {
        TreeLinkNode cur = root;
        TreeLinkNode head = null;//下层的first node
        TreeLinkNode prev = null;//上一个node

        while (cur != null){
            //结束时cur = head = null

            //this level
            while (cur != null){
                if (cur.left != null){
                    if (prev == null)
                        head = cur.left;
                    else
                        prev.next = cur.left;
                    prev = cur.left;

                }
                if (cur.right != null){
                    if (prev == null)
                        head = cur.right;
                    else
                        prev.next = cur.right;
                    prev = cur.right;
                }
                cur = cur.next;
            }

            //初始化next level
            cur = head;
            head = null;
            prev = null;
        }
    }
}
```
