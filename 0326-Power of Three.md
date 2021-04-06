难度：Easy  
思路：常规想法，将n一直除以3。  
```java
public class Solution {
    public boolean isPowerOfThree(int n) {
        if (n < 1) {
            return false;
        }

        while (n % 3 == 0) {
            n /= 3;
        }

        return n == 1;
    }
}
```
```
执行用时：17 ms, 在所有 Java 提交中击败了42.35%的用户
内存消耗：38 MB, 在所有 Java 提交中击败了92.35%的用户
```
时间复杂度：O(logn)。除数是用对数表示的。
空间复杂度：O(1)
