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
    public void postorder(TreeNode root, List<Integer> res)
    {
        if(root == null)
        {
            return;
        }
        postorder(root.left, res);
        postorder(root.right, res);
        res.add(root.val);
    }

    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<Integer>();
        postorder(root, res);
        return res;
    }
}
```
```
执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：36.6 MB, 在所有 Java 提交中击败了84.48%的用户
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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<Integer>();
        if(root == null)
        {
            return res;
        }
        Deque<TreeNode> stk = new LinkedList<TreeNode>();
        TreeNode prev = null;
        while(root != null || !stk.isEmpty())
        {
            while(root != null)
            {
                stk.push(root);
                root = root.left;
            }
            root = stk.pop();
            if(root.right == null || root.right == prev)
            {
                res.add(root.val);
                prev = root;
                root = null;
            }
            else
            {
                stk.push(root);
                root = root.right;    
            }         
        }
        return res;
    }
}
```
```
执行用时：1 ms, 在所有 Java 提交中击败了55.23%的用户
内存消耗：36.8 MB, 在所有 Java 提交中击败了37.15%的用户
```
时间复杂度：O(n)  
空间复杂度：O(n)
