# 官方题解-双指针法
使用双指针，左指针指向当前已经处理好的序列的尾部，右指针指向待处理序列的头部。  
右指针不断向右移动，每次右指针指向非零数，则将左右指针对应的数交换，同时左指针右移。  
注意到以下性质：  
左指针左边均为非零数；  
右指针左边直到左指针处均为零。  
因此每次交换，都是将左指针的零与右指针的非零数交换，且非零数的相对顺序并未改变。  
```java
class Solution {
    public void moveZeroes(int[] nums) {
        int n = nums.length, left = 0, right = 0;
        while (right < n) {
            if (nums[right] != 0) {
                swap(nums, left, right);
                left++;
            }
            right++;
        }
    }

    public void swap(int[] nums, int left, int right) {
        int temp = nums[left];
        nums[left] = nums[right];
        nums[right] = temp;
    }
}
```
```
执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：38.9 MB, 在所有 Java 提交中击败了19.11%的用户
```
时间复杂度：O(n)  
空间复杂度：O(1)
