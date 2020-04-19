# 法一：转置加翻转
```java
class Solution {
  public void rotate(int[][] matrix) {
    int n = matrix.length;

    // transpose matrix
    for (int i = 0; i < n; i++) {
      for (int j = i; j < n; j++) {
        int tmp = matrix[j][i];
        matrix[j][i] = matrix[i][j];
        matrix[i][j] = tmp;
      }
    }
    // reverse each row
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < n / 2; j++) {
        int tmp = matrix[i][j];
        matrix[i][j] = matrix[i][n - j - 1];
        matrix[i][n - j - 1] = tmp;
      }
    }
  }
}
```
```
Runtime: 0 ms, faster than 100.00% of Java online submissions for Rotate Image.
Memory Usage: 40.2 MB, less than 5.77% of Java online submissions for Rotate Image.
```
时间复杂度：O(N^2)  
空间复杂度：O(1)

# 法二：旋转四个矩形
只使用一次操作完成旋转，分成四个矩形。
![动图](https://pic.leetcode-cn.com/d2b8312ed463bceb9ac3feb88e00c70abc4edc02c55ade3fea4723e757e269d9-image.png)
```java
class Solution {
  public void rotate(int[][] matrix) {
    int n = matrix.length;
    for (int i = 0; i < n / 2 + n % 2; i++) {
      for (int j = 0; j < n / 2; j++) {
        int[] tmp = new int[4];
        int row = i;
        int col = j;
        for (int k = 0; k < 4; k++) {
          tmp[k] = matrix[row][col];
          int x = row;
          row = col;
          col = n - 1 - x;
        }
        for (int k = 0; k < 4; k++) {
          matrix[row][col] = tmp[(k + 3) % 4];
          int x = row;
          row = col;
          col = n - 1 - x;
        }
      }
    }
  }
}
```
```
Runtime: 0 ms, faster than 100.00% of Java online submissions for Rotate Image.
Memory Usage: 40.7 MB, less than 5.77% of Java online submissions for Rotate Image.
```
时间复杂度：O(N^2)  
空间复杂度：O(1)

# 法三：在单词循环中旋转4个矩形
思路与法二相同。
```java
class Solution {
  public void rotate(int[][] matrix) {
    int n = matrix.length;
    for (int i = 0; i < (n + 1) / 2; i ++) {
      for (int j = 0; j < n / 2; j++) {
        int temp = matrix[n - 1 - j][i];
        matrix[n - 1 - j][i] = matrix[n - 1 - i][n - j - 1];
        matrix[n - 1 - i][n - j - 1] = matrix[j][n - 1 -i];
        matrix[j][n - 1 - i] = matrix[i][j];
        matrix[i][j] = temp;
      }
    }
  }
}
```
```
Runtime: 0 ms, faster than 100.00% of Java online submissions for Rotate Image.
Memory Usage: 39.2 MB, less than 5.77% of Java online submissions for Rotate Image.
```
时间复杂度：O(N^2)  
空间复杂度：O(1)
