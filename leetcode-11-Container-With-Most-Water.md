### 题目

Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2.

大意是，给定n个数据，数据表示在某个位置距离Y轴上的高度，找到由两个纵轴与X轴能围成的容器，最大能装多少水。

### 思路

思路1：O(n*n) 的时间复杂度，查找每一个容器大小，并进行比对，但这种方法会超时。

思路2：开始我采用了动态规划的方式，但发现推导出的公式，还是得用前面的暴力方法来求解。后面，参考了其他人的实现，采用了双端逼近的方法来解决，设想这样一个前提，我们确定了右边界的情况下，来看左边界。我们指定左边界为i，考虑从 i 到 右边界的情况。在这些i到右边界的遍历中，如果高度比 height[i] 要小，那么就可以舍弃掉了，因为你的左边界 i 的高度比你高，距离还比你远。同样也可以这样思考左边界固定的情况。

### 代码示例

```java
public int maxArea(int[] height) {

  int maxValue = 0;

  int leftIndex = 0;
  int rightIndex = height.length - 1;

  while (leftIndex < rightIndex) {

    maxValue = Math.max(
        maxValue,
        Math.min(height[leftIndex], height[rightIndex]) * (rightIndex - leftIndex));

    if (height[leftIndex] > height[rightIndex]) {
      int tempRightValue = height[rightIndex];
      while (--rightIndex > leftIndex) {
        if (height[rightIndex] > tempRightValue) {
          break;
        }
      }
    } else {
      int tempLeftValue = height[leftIndex];
      while (++leftIndex < rightIndex) {
        if (height[leftIndex] > tempLeftValue) {
          break;
        }
      }
    }

  }

  return maxValue;
}
```
