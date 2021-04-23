难度：Medium  
思路：利用BST特性：BST的中序遍历是升序序列。  
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
    public ArrayList<Integer> inorder(TreeNode root, ArrayList<Integer> arr)
    {
        if(root == null)
        {
            return arr;
        }
        inorder(root.left, arr);
        arr.add(root.val);
        inorder(root.right, arr);
        return arr;
    }

    public int kthSmallest(TreeNode root, int k) {
     ArrayList<Integer> nums = inorder(root, new ArrayList<Integer>());
     return nums.get(k - 1);
    }
}
```
```
执行用时：1 ms, 在所有 Java 提交中击败了46.53%的用户
内存消耗：38.8 MB, 在所有 Java 提交中击败了22.35%的用户
```
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
    public int kthSmallest(TreeNode root, int k) {
        LinkedList<TreeNode> stack = new LinkedList<TreeNode>();

        while (true) 
        {
            while (root != null)
            {
                stack.add(root);
                root = root.left;
            }
            root = stack.removeLast();
            if(--k == 0)
            {
                return root.val;
            }
            root = root.right;
        }
    }
}
```
```
执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：38.1 MB, 在所有 Java 提交中击败了89.16%的用户
```
