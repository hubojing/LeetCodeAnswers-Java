# 官方题解
## 法一：优先队列
最大值问题，考虑优先队列（堆）。现将数组前k个元素放入优先队列中，向右移动窗口时，把新元素放入优先队列，此时堆顶元素就是堆的最大值。考虑这个最大值可能不在滑动窗口中，所以需要存储元素的索引，如果不在窗口内，则从优先队列中移除。
```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        PriorityQueue<int[]> pq = new PriorityQueue<int[]>(new Comparator<int[]>() {
            public int compare(int[] pair1, int[] pair2) {
                return pair1[0] != pair2[0] ? pair2[0] - pair1[0] : pair2[1] - pair1[1];
            }
        });
        for (int i = 0; i < k; ++i) {
            pq.offer(new int[]{nums[i], i});
        }
        int[] ans = new int[n - k + 1];
        ans[0] = pq.peek()[0];
        for (int i = k; i < n; ++i) {
            pq.offer(new int[]{nums[i], i});
            while (pq.peek()[1] <= i - k) {
                pq.poll();
            }
            ans[i - k + 1] = pq.peek()[0];
        }
        return ans;
    }
}
```
```
执行用时：114 ms, 在所有 Java 提交中击败了7.33%的用户
内存消耗：59.1 MB, 在所有 Java 提交中击败了11.97%的用户
```
## 法二：单调队列

## 法三：分块 + 预处理
