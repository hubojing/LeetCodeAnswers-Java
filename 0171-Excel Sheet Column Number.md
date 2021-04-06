思路：本题考的进制转换。  
而十六进制转为十进制即可。
```java
class Solution {
    public int titleToNumber(String s) {
        int ans = 0;
        for(int i=0;i<s.length();i++) {
            int num = s.charAt(i) - 'A' + 1;
            ans = ans * 26 + num;
        }
        return ans;
    }
}
```
```
执行用时：1 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：38.4 MB, 在所有 Java 提交中击败了59.70%的用户
```
