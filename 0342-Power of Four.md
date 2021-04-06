难度：Easy    
思路：借用2的幂的思路，先用n & (n - 1) == 0判断是不是2的幂，再用nums和3的取余来看是不是4的幂，为1是，为2不是。
```java
class Solution {
  public boolean isPowerOfFour(int num) {
    return (num > 0) && ((num & (num - 1)) == 0) && (num % 3 == 1);
  }
}
```
```
执行用时：1 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：35.6 MB, 在所有 Java 提交中击败了42.16%的用户
```
时间复杂度：O(1)
空间复杂度：O(1)
