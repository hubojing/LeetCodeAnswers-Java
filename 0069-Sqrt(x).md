难度：Easy  
思路：二分查找
```java
class Solution {
    public int mySqrt(int x) {
        int l = 0, r = x, ans = -1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if ((long) mid * mid <= x) {
                ans = mid;
                l = mid + 1;
            } else {
                r = mid - 1;
            }
        }
        return ans;
    }
}
```
```
执行用时：2 ms, 在所有 Java 提交中击败了44.76%的用户
内存消耗：35.4 MB, 在所有 Java 提交中击败了71.45%的用户
```
时间复杂度：O(logx)  
空间复杂度：O(1)
