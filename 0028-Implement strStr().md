难度： Easy
# 官方题解
# 法一：子串逐一比较
```java
class Solution {
  public int strStr(String haystack, String needle) {
    int L = needle.length(), n = haystack.length();

    for (int start = 0; start < n - L + 1; ++start) {
      if (haystack.substring(start, start + L).equals(needle)) {
        return start;
      }
    }
    return -1;
  }
}
```
```
执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：38.5 MB, 在所有 Java 提交中击败了28.10%的用户
```
时间复杂度：O((N−L)L)，其中 N 为 haystack 字符串的长度，L 为 needle 字符串的长度。内循环中比较字符串的复杂度为 L，总共需要比较 (N - L) 次。  
空间复杂度：O(1)

# 法二：双指针
上一个方法的缺陷是会将 haystack 所有长度为 L 的子串都与 needle 字符串比较，实际上是不需要这么做的。  
1. 只有子串的第一个字符跟 needle 字符串第一个字符相同的时候才需要比较。2. 可以一个字符一个字符比较，一旦不匹配了就立刻终止。  
算法：  
移动 pn 指针，直到 pn 所指向位置的字符与 needle 字符串第一个字符相等。  
通过 pn，pL，curr_len 计算匹配长度。  
如果完全匹配（即 curr_len == L），返回匹配子串的起始坐标（即 pn - L）。  
如果不完全匹配，回溯。使 pn = pn - curr_len + 1， pL = 0， curr_len = 0。  
```java
class Solution {
  public int strStr(String haystack, String needle) {
    int L = needle.length(), n = haystack.length();
    if (L == 0) return 0;

    int pn = 0;
    while (pn < n - L + 1) {
      // find the position of the first needle character
      // in the haystack string
      while (pn < n - L + 1 && haystack.charAt(pn) != needle.charAt(0)) ++pn;

      // compute the max match string
      int currLen = 0, pL = 0;
      while (pL < L && pn < n && haystack.charAt(pn) == needle.charAt(pL)) {
        ++pn;
        ++pL;
        ++currLen;
      }

      // if the whole needle string is found,
      // return its start position
      if (currLen == L) return pn - L;

      // otherwise, backtrack
      pn = pn - currLen + 1;
    }
    return -1;
  }
}
```
```
执行用时：2 ms, 在所有 Java 提交中击败了51.61%的用户
内存消耗：37 MB, 在所有 Java 提交中击败了73.69%的用户
```
时间复杂度：最坏时间复杂度为 O((N−L)L)，最优时间复杂度为 O(N)。  
空间复杂度：O(1)。
# 法三： Rabin Karp
思路：先生成窗口内子串的哈希码，然后再跟 needle 字符串的哈希码做比较。  
如何在常数时间生成子串的哈希码？  
滚动哈希：常数时间生成哈希码  
如何避免溢出  
设置数值上限来避免溢出。设置数值上限可以用取模的方式，即用 h % modulus 来代替原本的哈希值。  

算法：  
1. 计算子字符串 haystack.substring(0, L) 和 needle.substring(0, L) 的哈希值。  
2. 从起始位置开始遍历：从第一个字符遍历到第 N - L 个字符。  
- 根据前一个哈希值计算滚动哈希。  
- 如果子字符串哈希值与 needle 字符串哈希值相等，返回滑动窗口起始位置。  
3. 返回 -1，这时候 haystack 字符串中不存在 needle 字符串。  
```java
class Solution {
  // function to convert character to integer
  public int charToInt(int idx, String s) {
    return (int)s.charAt(idx) - (int)'a';
  }

  public int strStr(String haystack, String needle) {
    int L = needle.length(), n = haystack.length();
    if (L > n) return -1;

    // base value for the rolling hash function
    int a = 26;
    // modulus value for the rolling hash function to avoid overflow
    long modulus = (long)Math.pow(2, 31);

    // compute the hash of strings haystack[:L], needle[:L]
    long h = 0, ref_h = 0;
    for (int i = 0; i < L; ++i) {
      h = (h * a + charToInt(i, haystack)) % modulus;
      ref_h = (ref_h * a + charToInt(i, needle)) % modulus;
    }
    if (h == ref_h) return 0;

    // const value to be used often : a**L % modulus
    long aL = 1;
    for (int i = 1; i <= L; ++i) aL = (aL * a) % modulus;

    for (int start = 1; start < n - L + 1; ++start) {
      // compute rolling hash in O(1) time
      h = (h * a - charToInt(start - 1, haystack) * aL
              + charToInt(start + L - 1, haystack)) % modulus;
      if (h == ref_h) return start;
    }
    return -1;
  }
}
```
```
执行用时：4 ms, 在所有 Java 提交中击败了27.05%的用户
内存消耗：36.9 MB, 在所有 Java 提交中击败了80.38%的用户
```
时间复杂度：O(N)，计算 needle 字符串的哈希值需要 O(L) 时间，之后需要执行 (N−L) 次循环，每次循环的计算复杂度为常数。

空间复杂度：O(1)。
