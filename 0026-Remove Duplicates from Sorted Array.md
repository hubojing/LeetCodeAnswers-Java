官方Solution
# 双指针法
i慢指针，j快指针。由于原排列已经排序，所以i从0开始，j从1开始，如果i的值等于j的值，则j后移一位。如果i不等于j的值，则i后移一位，并且用nuns[i]记录此时nums[j]的值。然后j继续后移。
```java
class Solution {
    public int removeDuplicates(int[] nums) {
       if(nums.length == 0) return 0;
        int i = 0;
        for(int j = 1; j < nums.length; j++){
            if(nums[j] != nums[i]){
                i++;
                nums[i] = nums[j];
            }
        }
        return i + 1;
    }
}
```
```
Runtime: 1 ms, faster than 97.51% of Java online submissions for Remove Duplicates from Sorted Array.
Memory Usage: 38.8 MB, less than 99.47% of Java online submissions for Remove Duplicates from Sorted Array.
```
