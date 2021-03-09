难度：Medium  
# 官方题解
思路：动态规划  
做此题前可先做第53题。  
和53题的区别在于，对负数的处理。由于负负得正，所以负的越多乘积可能越大。所以要比较三个值：当前值、当前值与前面最大值乘积、当前值与前面最小值乘积，取三个数中的最大值。
```java
class Solution {
    public int maxProduct(int[] nums) {
        int maxF = nums[0], minF = nums[0], ans = nums[0];
        int length = nums.length;
        for (int i = 1; i < length; ++i) {
            int mx = maxF, mn = minF;
            maxF = Math.max(mx * nums[i], Math.max(nums[i], mn * nums[i]));
            minF = Math.min(mn * nums[i], Math.min(nums[i], mx * nums[i]));
            ans = Math.max(maxF, ans);
        }
        return ans;
    }
}
```
```
执行用时：2 ms, 在所有 Java 提交中击败了87.98%的用户
内存消耗：38.3 MB, 在所有 Java 提交中击败了42.69%的用户
```
时间复杂度：O(n)  
空间复杂度：O(1)
