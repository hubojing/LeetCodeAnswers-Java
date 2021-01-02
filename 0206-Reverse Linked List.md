# 官方题解
## 法一：迭代
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode curr = head;
        while (curr != null) {
            ListNode nextTemp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = nextTemp;
        }
        return prev;
    }
}
```
```
执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：37.8 MB, 在所有 Java 提交中击败了96.93%的用户
```
时间复杂度：O(n)
空间复杂度：O(1)

## 法二：递归
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode p = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return p;
    }
}
```
```
执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：38.7 MB, 在所有 Java 提交中击败了13.63%的用户
```
时间复杂度：O(n)
空间复杂度：O(n)
