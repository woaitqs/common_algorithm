### 题目

Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words. You may assume the dictionary does not contain duplicate words.

For example, given
s = "leetcode",
dict = ["leet", "code"].

Return true because "leetcode" can be segmented as "leet code".

给定一个字符串和相应的字典，判断这个字符串能否有这个字典里面的词完全拼接出来。

### 思路

思路一：暴力比较每一个字符串，这样时间会超时。
思路二：利用动态规划的方法来进行计算。

dp[i] 表示从0到i这样的字符串，能否由字典里面的词拼接出来。
那么 dp[i +1] 则是 dp[x] & (x,i+1) 的值, 其中 x 取值 0 到 i。
通俗的解释就是dp[x]是否成立，并且剩下的字符串也要能有字典里面的字符组成。

### 代码示例

```java
public class Solution {
  public boolean wordBreak(String s, List<String> wordDict) {

    boolean[] dpValue = new boolean[s.length() + 1];
    dpValue[0] = true;
    for (int i = 1; i <= s.length(); i++) {
      boolean iterValue = false;
      for (int j = 0; j < i; j++) {
        if (dpValue[j] && hasWord(s.substring(j, i), wordDict)) {
          iterValue = true;
          break;
        }
      }
      dpValue[i] = iterValue;
    }
    return dpValue[s.length()];

  }

  private boolean hasWord(String compare, List<String> wordDict) {
    for (String word : wordDict) {
      if (word.equals(compare)) {
        return true;
      }
    }
    return false;
  }
}
```
