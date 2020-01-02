说实话这个题干我读了几遍才懂是什么意思……=_=
# 法一：暴力解法
不可取  
时间复杂度：O(n!)  
空间复杂度：O(n)  
# 法二：一遍扫描法
官方解释我看了很久都没明白，这个动图一出现，立刻就明白了。  
[动图请点击此处](https://leetcode.com/media/original_images/31_Next_Permutation.gif)  
这个题我认为关键就在于明白怎么调整才是刚好大一点，整个逻辑要疏通。  
```java
class Solution {
    public void nextPermutation(int[] nums) {
        int i = nums.length - 2;
        while (i >= 0 && nums[i + 1] <= nums[i]) {
            i--;
        }
        if (i >= 0) {
            int j = nums.length - 1;
            while (j >= 0 && nums[j] <= nums[i]) {
                j--;
            }
            swap(nums, i, j);
        }
        reverse(nums, i + 1);
    }

    private void reverse(int[] nums, int start) {
        int i = start, j = nums.length - 1;
        while (i < j) {
            swap(nums, i, j);
            i++;
            j--;
        }
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```
```
Runtime: 0 ms, faster than 100.00% of Java online submissions for Next Permutation.
Memory Usage: 40 MB, less than 48.00% of Java online submissions for Next Permutation.
```
