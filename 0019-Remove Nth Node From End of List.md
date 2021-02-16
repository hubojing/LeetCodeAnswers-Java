难度：Medium
# 官方题解
## 法一：计算链表长度
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0, head);
        int length = getLength(head);
        ListNode cur = dummy;
        for (int i = 1; i < length - n + 1; ++i) {
            cur = cur.next;
        }
        cur.next = cur.next.next;
        ListNode ans = dummy.next;
        return ans;
    }

    public int getLength(ListNode head) {
        int length = 0;
        while (head != null) {
            ++length;
            head = head.next;
        }
        return length;
    }
}
```
```
执行用时：1 ms, 在所有 Java 提交中击败了17.90%的用户
内存消耗：36.6 MB, 在所有 Java 提交中击败了23.98%的用户
```
时间复杂度：O(L)，其中 L 是链表的长度。  
空间复杂度：O(1)。

## 法二：栈
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0, head);
        Deque<ListNode> stack = new LinkedList<ListNode>();
        ListNode cur = dummy;
        while (cur != null) {
            stack.push(cur);
            cur = cur.next;
        }
        for (int i = 0; i < n; ++i) {
            stack.pop();
        }
        ListNode prev = stack.peek();
        prev.next = prev.next.next;
        ListNode ans = dummy.next;
        return ans;
    }
}
```
```
执行用时：1 ms, 在所有 Java 提交中击败了17.90%的用户
内存消耗：36.3 MB, 在所有 Java 提交中击败了79.29%的用户
```
时间复杂度：O(L)，其中 L 是链表的长度。  
空间复杂度：O(L)，其中 L 是链表的长度。

## 法三：双指针
思路：由于需要找到倒数第 n 个节点，因此可以使用两个指针 first 和 second 同时对链表进行遍历，并且 first 比 second 超前 n 个节点。当 first 遍历到链表的末尾时，second 就恰好处于倒数第 n 个节点。
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0, head);
        ListNode first = head;
        ListNode second = dummy;
        for (int i = 0; i < n; ++i) {
            first = first.next;
        }
        while (first != null) {
            first = first.next;
            second = second.next;
        }
        second.next = second.next.next;
        ListNode ans = dummy.next;
        return ans;
    }
}
```
```
执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：36.2 MB, 在所有 Java 提交中击败了86.71%的用户
```
时间复杂度：O(L)，其中 L 是链表的长度。  
空间复杂度：O(1)。
