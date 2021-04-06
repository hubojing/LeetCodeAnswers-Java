难度：Easy  
思路：位运算。  
n & n - 1 去掉n最低位的二进制1
```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        return n > 0 && (n & (n - 1)) == 0;
    }
}
```
```
执行用时：1 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：35.5 MB, 在所有 Java 提交中击败了63.69%的用户
```
