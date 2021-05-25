# 模拟
```java
class Solution {
    public String addBinary(String a, String b) {
        StringBuffer ans = new StringBuffer();

        int n = Math.max(a.length(), b.length()), carry = 0;
        for (int i = 0; i < n; ++i) {
            carry += i < a.length() ? (a.charAt(a.length() - 1 - i) - '0') : 0;
            carry += i <b.length() ? (b.charAt(b.length() - 1 - i) - '0') : 0;
            ans.append((char)(carry % 2 + '0'));
            carry /= 2;
        }

        if (carry > 0) {
            ans.append('1');
        }
        ans.reverse();

        return ans.toString();
    }
}
```
```
执行用时：3 ms, 在所有 Java 提交中击败了54.83%的用户
内存消耗：37.9 MB, 在所有 Java 提交中击败了85.64%的用户
```
时间复杂度：O(n)  
空间复杂度：O(1)
