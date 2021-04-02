这题太秀了...  
难度: Easy  
思路：放弃固定思维，没传入head，就直接把后面的值赋给当前值，并改变链表指向就行了。  
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
    public void deleteNode(ListNode node) {
        node.val = node.next.val;
        node.next = node.next.next;
    }   
}
```
```
执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：38 MB, 在所有 Java 提交中击败了23.70%的用户
```
时间和空间复杂度都是：O(1)
