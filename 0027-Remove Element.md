官方题解  
# 法一：双指针法
i慢指针，j快指针。因为题目中有句话"The order of elements can be changed. It doesn't matter what you leave beyond the new length."，好好利用这句话，用i记录改变后的数组长度。
```java
class Solution {
	public int removeElement(int[] nums, int val) {
		int i = 0;
		for (int j = 0; j < nums.length; j++) {
			if (nums[j] != val) {
				nums[i] = nums[j];
				i++;
			}
		}
		return i;
	}
}
```
```
Runtime: 0 ms, faster than 100.00% of Java online submissions for Remove Element.
Memory Usage: 35.4 MB, less than 100.00% of Java online submissions for Remove Element.
```
时间复杂度：O(n)  
空间复杂度：O(1)

# 法二：双指针法-当被删除的数比较少时
上面解法有不必要的复制过程（不等于val时都进行了复制），换个角度想，当要删除的数比较少时，等于val才进行处理，就会更快些。把要删除的数和最后一个数交换，然后再令新的数组长度减一即可。注意最后一个数可能也是要删除的数，不过这在下一次循环中会被剔除。
```java
class Solution {
	public int removeElement(int[] nums, int val) {
		int i = 0;
		int n = nums.length;
		while (i < n) {
			if (nums[i] == val) {
				nums[i] = nums[n - 1];
				n--;
			} else {
				i++;
			}
		}
		return n;
	}
}
```
```
Runtime: 0 ms, faster than 100.00% of Java online submissions for Remove Element.
Memory Usage: 36.4 MB, less than 100.00% of Java online submissions for Remove Element.
```
时间复杂度：O(n)  
空间复杂度：O(1)
