### 题目

  > Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.
  
  ![histogram area](http://o8p68x17d.bkt.clouddn.com/histogram_area.png)
  
  给定一个非负整数的数组，这个数组如上图一样，可以用直方图的形式来展示，求能够组成的最大矩形的面积。在上图中，红色矩形的那一块就是最大的面积。

### 解答：

  这个题目也是对栈的利用。我们先想想一个递增的序列，在这种情况下，矩形最大的面积一定是可以连续计算的，但一定遇到下跌的数字，出现了断层，这一块区域就不能连续计算了。由此我们通过栈的方式，来维持一个递增序列，当遇到下降时就进行计算一次。这里的逻辑相对复杂，大家需要多花一些时间来理解。

### 代码示例

```java
public int largestRectangleArea(int[] heights) {
    int maxArea = 0;
    List<Integer> newHeights = new ArrayList<>();
    for (int item : heights) {
      newHeights.add(item);
    }
    newHeights.add(0);

    Stack<Integer> areaIndexs = new Stack<>();

    int index = 0;
    while (index < newHeights.size()) {
      if (areaIndexs.isEmpty() || newHeights.get(index) > newHeights.get(areaIndexs.peek())) {
        // push index to stacks.
        areaIndexs.push(index);
        index ++;
      } else {
        int top = areaIndexs.peek();
        areaIndexs.pop();
        maxArea = Math.max(
            maxArea,
            newHeights.get(top) * (areaIndexs.isEmpty() ? index : index - areaIndexs.peek() - 1));
      }
    }
    return maxArea;
  }
```