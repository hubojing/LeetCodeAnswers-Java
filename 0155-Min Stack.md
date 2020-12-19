# 官方题解
设计一个数据结构，使得每个元素 a 与其相应的最小值 m 时刻保持一一对应。因此可以使用一个辅助栈，与元素栈同步插入与删除，用于存储与每个元素对应的最小值。  
- 当一个元素要入栈时，取当前辅助栈的栈顶存储的最小值，与当前元素比较得出最小值，将这个最小值插入辅助栈中；
- 当一个元素要出栈时，我们把辅助栈的栈顶元素也一并弹出；
- 在任意一个时刻，栈内元素的最小值就存储在辅助栈的栈顶元素中。
```java
class MinStack {
    Deque<Integer> xStack;
    Deque<Integer> minStack;

    public MinStack() {
        xStack = new LinkedList<Integer>();
        minStack = new LinkedList<Integer>();
        minStack.push(Integer.MAX_VALUE);
    }
    
    public void push(int x) {
        xStack.push(x);
        minStack.push(Math.min(minStack.peek(), x));
    }
    
    public void pop() {
        xStack.pop();
        minStack.pop();
    }
    
    public int top() {
        return xStack.peek();
    }
    
    public int getMin() {
        return minStack.peek();
    }
}
```
```
执行用时：7 ms, 在所有 Java 提交中击败了77.58%的用户
内存消耗：40.2 MB, 在所有 Java 提交中击败了73.21%的用户
```
时间复杂度：O(1)  
空间复杂度：O(n)
