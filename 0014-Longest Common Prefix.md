# 法一：纵向扫描
每个字符都从前往后开始遍历，不同就停止。
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) {
            return "";
        }
        int length = strs[0].length();
        int count = strs.length;
        for (int i = 0; i < length; i++) {
            char c = strs[0].charAt(i);
            for (int j = 1; j < count; j++) {
                if (i == strs[j].length() || strs[j].charAt(i) != c) {
                    return strs[0].substring(0, i);
                }
            }
        }
        return strs[0];
    }
}

```
```
执行用时：2 ms, 在所有 Java 提交中击败了30.63%的用户
内存消耗：36.5 MB, 在所有 Java 提交中击败了59.34%的用户
```
时间复杂度：O(mn)  
空间复杂度：O(1)
# 法二：横向扫描
每两个一比较，取公共前缀；再取该公共前缀和下一个字符串的公共前缀。
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) {
            return "";
        }
        String prefix = strs[0];
        int count = strs.length;
        for (int i = 1; i < count; i++) {
            prefix = longestCommonPrefix(prefix, strs[i]);
            if (prefix.length() == 0) {
                break;
            }
        }
        return prefix;
    }

    public String longestCommonPrefix(String str1, String str2) {
        int length = Math.min(str1.length(), str2.length());
        int index = 0;
        while (index < length && str1.charAt(index) == str2.charAt(index)) {
            index++;
        }
        return str1.substring(0, index);
    }
}
```
```
执行用时：1 ms, 在所有 Java 提交中击败了85.02%的用户
内存消耗：36.5 MB, 在所有 Java 提交中击败了61.78%的用户
```
时间复杂度：O(mn)  
空间复杂度：O(1)
