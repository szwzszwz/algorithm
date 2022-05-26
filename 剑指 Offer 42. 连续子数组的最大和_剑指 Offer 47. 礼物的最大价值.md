#### [剑指 Offer 42. 连续子数组的最大和](https://leetcode.cn/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

**示例1:**

```
输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

**提示：**

- `1 <= arr.length <= 10^5`
- `-100 <= arr[i] <= 100`

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int[] sum = new int[nums.length];
        for(int i = 0;i < nums.length;i++)
        {
            int max = nums[i];
            if(i > 0 && nums[i] < sum[i - 1] + nums[i])
                sum[i] = sum[i - 1] + nums[i];
            else
                sum[i] = nums[i];
        }

        int max = Integer.MIN_VALUE;
        for(int i = 0;i < sum.length;i++)
            if(sum[i] > max)
                max = sum[i];
        
        return max;
    }
}
```

解题思路：

用数组来存储到每一位的最大值，取（当前的数，上一个sum值）中的更大值放在新的数组。

___

#### [剑指 Offer 47. 礼物的最大价值](https://leetcode.cn/problems/li-wu-de-zui-da-jie-zhi-lcof/)

在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

**示例 1:**

```
输入: 
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 12
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物
```

提示：

- `0 < grid.length <= 200`
- `0 < grid[0].length <= 200`

```java
class Solution {
    public int maxValue(int[][] grid) {
        int[][] nums = new int[grid.length][grid[0].length];
        nums[0][0] = grid[0][0];
        int max = Integer.MIN_VALUE;
        for(int i = 0;i < grid.length;i++)
        {
            for(int j = 0;j < grid[0].length;j++)
            {
                if(i - 1 >= 0 && j - 1 >= 0 && nums[i - 1][j] > nums[i][j - 1])
                    nums[i][j] = grid[i][j] + nums[i - 1][j];
                else if(i - 1 >= 0 && j - 1 >= 0 && nums[i - 1][j] <= nums[i][j - 1])
                    nums[i][j] = grid[i][j] + nums[i][j - 1];
                else if(i - 1 >= 0 && j - 1 < 0)
                    nums[i][j] = grid[i][j] + nums[i - 1][j];
                else if(i - 1 < 0 && j - 1 >= 0)
                    nums[i][j] = grid[i][j] + nums[i][j - 1];
                if(nums[i][j] > max)
                    max = nums[i][j];
            }
        }
        return max;
    }
}
```

解题思路：将上一道题的一维思路扩展到二位即可