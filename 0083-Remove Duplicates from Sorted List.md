难度：Easy  
思路：由于链表有序，重复元素靠在一起。只需要判断一下并删除就好。  
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
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) {
            return head;
        }

        ListNode cur = head;
        while (cur.next != null) {
            if (cur.val == cur.next.val) {
                cur.next = cur.next.next;
            } else {
                cur = cur.next;
            }
        }

        return head;
    }
}
```
```
执行用时：1 ms, 在所有 Java 提交中击败了34.60%的用户
内存消耗：37.7 MB, 在所有 Java 提交中击败了88.10%的用户
```
时间复杂度：O(n)  
空间复杂度：O(1)
