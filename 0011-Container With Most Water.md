官方题解
解法一：暴力解法
```java
public class Solution {
    public int maxArea(int[] height) {
        int maxarea = 0;
        for (int i = 0; i < height.length; i++)
            for (int j = i + 1; j < height.length; j++)
                maxarea = Math.max(maxarea, Math.min(height[i], height[j]) * (j - i));
        return maxarea;
    }
}
```
```
Runtime: 212 ms, faster than 10.27% of Java online submissions for Container With Most Water.
Memory Usage: 39.7 MB, less than 95.51% of Java online submissions for Container With Most Water.
```
解法二：双指针法
```java
public class Solution {
    public int maxArea(int[] height) {
        int maxarea = 0, l = 0, r = height.length - 1;
        while (l < r) {
            maxarea = Math.max(maxarea, Math.min(height[l], height[r]) * (r - l));
            if (height[l] < height[r])
                l++;
            else
                r--;
        }
        return maxarea;
    }
}
```
```
Runtime: 2 ms, faster than 94.86% of Java online submissions for Container With Most Water.
Memory Usage: 39.1 MB, less than 100.00% of Java online submissions for Container With Most Water.
```
