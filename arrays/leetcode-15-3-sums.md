### 题目

Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note: The solution set must not contain duplicate triplets.

> For example, given array S = [-1, 0, 1, 2, -1, -4],
> 
> A solution set is:
>
> [
>
> &nbsp;&nbsp;&nbsp;[-1, 0, 1],
>
> &nbsp;&nbsp;&nbsp;[-1, -1, 2]
>
> ]

找到所有和为0的，由三个数字组成的数组。注意，不能重复。

### 思路

我们这么分析下这个问题，最暴力的方式就是遍历出所有可能的由三个数字组成的数组，判断他们的和是否等于0，但这样的时间复杂度在o(n^3)上面。
如果要优化这种情况，那么就需要对遍历的情况进行优化，怎么优化呢？就是人为地引入一些限制条件，答案就是「排序」。对于一个排序好的数组，这个问题
可以转换为，给定一个数字，在这个数字对应的Index之后的数字里面，找寻两个数字，使得他们的和为 `0 - nums[index]`。而找到两个数字和为 `0 - nums[index]`，
在一个排好序的数组里面，只需要 o(n) 的时间。这样下来，时间复杂度就被降低到 o(n^2) 了。这个题目的难点不在于算法复杂度上面，而是在于如何`去重`上面。

`去重` 在一个排好序的数组里面，可以做到相对简单些，比较过的数字，不再进行比较即可。

额外地提及一下，找到两个数字和为 `0 - nums[index]`的算法，可以用双端逼近的做法来实现，具体参考下面的算法。

### 代码示例

```java
public class Solution {

    public List<List<Integer>> threeSum(int[] nums) {

        // [-1,-1,0,1]

        List<List<Integer>> result = new ArrayList<>();

        if (nums == null || nums.length < 3) {
            return result;
        }

        Arrays.sort(nums);

        for (int index = 0; index < nums.length - 2; index++) {

            if (index > 0 && nums[index] == nums[index - 1]) {
                continue;
            }

            // search the left array to find if find two sums match target
            int left = index + 1;
            int right = nums.length - 1;

            int target = 0 - nums[index];

            while (left < right) {
                if (nums[left] + nums[right] == target) {
                    List<Integer> possible = new ArrayList<>();
                    possible.add(nums[index]);
                    possible.add(nums[left]);
                    possible.add(nums[right]);
                    result.add(possible);
                    left++;
                    right--;
                    while (left < nums.length - 1 && nums[left] == nums[left - 1]) {
                        left++;
                    }
                    while (right > left && nums[right] == nums[right + 1]) {
                        right--;
                    }
                } else if (nums[left] + nums[right] + nums[index] < 0) {
                    left++;
                } else {
                    right--;
                }
            }

        }

        return result;

    }

}

```