为了找到最左边（或者最右边）包含`target`的下标（而不是找到就返回`true`），在找到一个`target`后继续搜索，直到`lo == hi`且它们在某个`target`值处下标相同。  
`left`参数的引入，表明在遇到`target == nums[mid]`时应该做什么。如果`left`为`true`，那么递归查询左区间，否则递归右区间。比如，如果在下标为`i`处遇到了`target`，最左边的`target`一定不会出现在下标大于`i`的位置，所以不需要考虑右子区间。当求最右下标时，道理同样适用。
```java
class Solution {
    // returns leftmost (or rightmost) index at which `target` should be
    // inserted in sorted array `nums` via binary search.
    private int extremeInsertionIndex(int[] nums, int target, boolean left) {
        int lo = 0;
        int hi = nums.length;

        while (lo < hi) {
            int mid = (lo + hi) / 2;
            if (nums[mid] > target || (left && target == nums[mid])) {
                hi = mid;
            }
            else {
                lo = mid+1;
            }
        }

        return lo;
    }

    public int[] searchRange(int[] nums, int target) {
        int[] targetRange = {-1, -1};

        int leftIdx = extremeInsertionIndex(nums, target, true);

        // assert that `leftIdx` is within the array bounds and that `target`
        // is actually in `nums`.
        if (leftIdx == nums.length || nums[leftIdx] != target) {
            return targetRange;
        }

        targetRange[0] = leftIdx;
        targetRange[1] = extremeInsertionIndex(nums, target, false)-1;

        return targetRange;
    }
}
```
```
Runtime: 0 ms, faster than 100.00% of Java online submissions for Find First and Last Position of Element in Sorted Array.
Memory Usage: 47.4 MB, less than 6.38% of Java online submissions for Find First and Last Position of Element in Sorted Array.
```
