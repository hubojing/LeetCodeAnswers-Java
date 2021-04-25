难度：Medium  
# 法一：递归
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public void inorder(TreeNode root, List<Integer> list)
    {
        if(root == null)
        {
            return;
        }
        inorder(root.left, list);
        list.add(root.val);
        inorder(root.right, list);
    }
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<Integer>();
        inorder(root, list);
        return list;
    }
}
```
```
执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：36.5 MB, 在所有 Java 提交中击败了87.80%的用户
```
时间复杂度：O(n)  
空间复杂度：O(n)
# 法二：迭代
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<Integer>();
        Deque<TreeNode> stk = new LinkedList<TreeNode>();
        while (root != null || !stk.isEmpty())
        {
            while (root != null)
            {
                stk.push(root);
                root = root.left;
            }
            root = stk.pop();
            res.add(root.val);
            root = root.right;
        }
        return res;
    }
}
```
```
执行用时：1 ms, 在所有 Java 提交中击败了43.09%的用户
内存消耗：36.6 MB, 在所有 Java 提交中击败了71.50%的用户
```
时间复杂度：O(n)  
空间复杂度：O(n)
