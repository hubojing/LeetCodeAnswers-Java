难度：medium
# 官方题解
思路：动态规划  
dp[0]表示空字符串是否可以被分割；  
dp[1]表示前1个字符串是否可以被分割；  
dp[2]表示前2个字符串是否可以被分割；  
...  
dp[s.length()]表示整体字符串全部可以被分割。  

if语句的理解：  
为了验证前i个字符是否可以被分割，遍历前i个字符，j作为分割点；  
dp[j]表示前j个字符串是否可以被分割，由于j小于i，故dp[j]是已知值，只需考虑j后面的是否在字典里，若两部分都是true，则dp[i]为true。  
```java
public class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        Set<String> wordDictSet = new HashSet(wordDict);
        boolean[] dp = new boolean[s.length() + 1];
        dp[0] = true;
        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && wordDictSet.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[s.length()];
    }
}
```
```
执行用时: 9 ms，超过了59%的java提交记录
内存消耗: 39 MB，超过了23%的java提交记录
```
时间复杂度：O(n^2)  
空间复杂度：O(n)

