### 题目

  Determine whether an integer is a palindrome. Do this without extra space.

### 解答：

  1. 首先判断一个数字的个数，通过除以10的次数来获取。
  2. 实现一个取每个数中特定位置的数字的算法
  3. 判断其从开始到 Math.floor(n/2)，与其对应的是否相等。

### 代码示例

```java
public class Solution {
  public boolean isPalindrome(int x) {
    if (x < 0) {
      return false;
    }
    int nums = 1;
    int tempValue = x;
    while (tempValue / 10 > 0) {
      tempValue /= 10;
      nums++;
    }

    for (int i = 0; i < nums / 2; i++) {
      if (getSpecDigit(x, i) != getSpecDigit(x, nums - i - 1)) {
        return false;
      }
    }

    return true;

  }

  private static int getSpecDigit(int x, int n) {
    return (x / (int) Math.pow(10, n)) % 10;
  }
}
```
