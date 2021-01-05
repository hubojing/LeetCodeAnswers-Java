# 官方题解
思路就是递归。
从根节点开始，递归地对树进行遍历，并从叶子结点先开始翻转。如果当前遍历到的节点 root 的左右两棵子树都已经翻转，那么只需要交换两棵子树的位置，即可完成以 root 为根节点的整棵子树的翻转。

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return null;
        }
        TreeNode left = invertTree(root.left);
        TreeNode right = invertTree(root.right);
        root.left = right;
        root.right = left;
        return root;
    }
}
```
```
执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：35.9 MB, 在所有 Java 提交中击败了40.83%的用户
```
时间复杂度：O(N)
空间复杂度：O(N)
