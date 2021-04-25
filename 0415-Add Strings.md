难度：Easy  
思路：模拟竖式加法。技巧：当前下标处于负数的时候返回 0，等价于对位数较短的数字进行了补零操作。
```java
class Solution {
    public String addStrings(String num1, String num2) {
        int i = num1.length() - 1, j = num2.length() - 1, add = 0;
        StringBuffer ans = new StringBuffer();
        while (i >= 0 || j >= 0 || add != 0)
        {
            int x = i >= 0 ? num1.charAt(i) - '0' : 0;
            int y = j >= 0 ? num2.charAt(j) - '0' : 0;
            int result = x + y + add;
            ans.append(result % 10);
            add = result / 10;
            i--;
            j--;
        }
        ans.reverse();
        return ans.toString();
    }
}
```
```
执行用时：3 ms, 在所有 Java 提交中击败了65.42%的用户
内存消耗：38.6 MB, 在所有 Java 提交中击败了44.12%的用户
```
