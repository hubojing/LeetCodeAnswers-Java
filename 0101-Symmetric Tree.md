# 官方题解
## 法一：递归
如果同时满足下面的条件，两个树互为镜像：
- 它们的两个根结点具有相同的值
- 每个树的右子树都与另一个树的左子树镜像对称
可以实现这样一个递归函数，通过「同步移动」两个指针的方法来遍历这棵树，p 指针和 q 指针一开始都指向这棵树的根，随后 p 右移时，q 左移，p 左移时，q 右移。每次检查当前 p 和 q 节点的值是否相等，如果相等再判断左右子树是否对称。
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
    public boolean isSymmetric(TreeNode root) {
        return check(root, root);
    }

    public boolean check(TreeNode p, TreeNode q) {
        if (p == null && q == null) {
            return true;
        }
        if (p == null || q == null) {
            return false;
        }
        return p.val == q.val && check(p.left, q.right) && check(p.right, q.left);
    }
}
```
```
执行用时：0 ms, 在所有 Java 提交中击败了 100% 的用户
内存消耗：36.4 MB, 在所有 Java 提交中击败了 89%的用户
```
时间复杂度：O(n)  
空间复杂度：O(n)

## 法二：迭代
首先引入一个队列，这是把递归程序改写成迭代程序的常用方法。初始化时把根节点入队两次。每次提取两个结点并比较它们的值（队列中每两个连续的结点应该是相等的，而且它们的子树互为镜像），然后将两个结点的左右子结点按相反的顺序插入队列中。当队列为空时，或者检测到树不对称（即从队列中取出两个不相等的连续结点）时，该算法结束。
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
    public boolean isSymmetric(TreeNode root) {
        return check(root, root);
    }

    public boolean check(TreeNode u, TreeNode v) {
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.offer(u);
        q.offer(v);
        while (!q.isEmpty()) {
            u = q.poll();
            v = q.poll();
            if (u == null && v == null) {
                continue;
            }
            if ((u == null || v == null) || (u.val != v.val)) {
                return false;
            }

            q.offer(u.left);
            q.offer(v.right);

            q.offer(u.right);
            q.offer(v.left);
        }
        return true;
    }
}
```
```
执行用时：1 ms, 在所有 Java 提交中击败了 29% 的用户
内存消耗：37.8 MB, 在所有 Java 提交中击败了 18%的用户
```
时间复杂度：O(n)  
空间复杂度：O(n)
