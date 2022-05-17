#### [剑指 Offer 03. 数组中重复的数字](https://leetcode.cn/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

找出数组中重复的数字。

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

**示例 1：**

```
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```

**限制：**

```
2 <= n <= 100000
```

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        int[] num = new int[nums.length];
        int i;
        for(i = 0;i < nums.length;i++)
            num[i] = -1;
        for(i = 0;i < nums.length;i++)
        {
            if(num[nums[i]] == nums[i])
                break;
            num[nums[i]] = nums[i];
        }

        return nums[i];
    }
}
```

解题思路：创建一个新的数组，所有值赋值为-1。出现第一次赋值，出现第二次直接返回

___

#### [剑指 Offer 53 - I. 在排序数组中查找数字 I](https://leetcode.cn/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

统计一个数字在排序数组中出现的次数。

**示例 1:**

```
输入: nums = [5,7,7,8,8,10], target = 8
输出: 2
```

**示例 2:**

```
输入: nums = [5,7,7,8,8,10], target = 6
输出: 0
```

**提示：**

- `0 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`
- `nums` 是一个非递减数组
- `-109 <= target <= 109`

```java
class Solution {
    public int search(int[] nums, int target) {
        int j = 0;
        for(int i = 0;i < nums.length;i++)
            if(nums[i] == target)
                j++;
        
        return j;
    }
}
```

解题思路：排好序的一串数字，但找到第一个target的时候开始计数，直到不是target的时候。

___

#### [剑指 Offer 53 - II. 0～n-1中缺失的数字](https://leetcode.cn/problems/que-shi-de-shu-zi-lcof/)

一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

**示例 1:**

```
输入: [0,1,3]
输出: 2
```

**示例 2:**

```
输入: [0,1,2,3,4,5,6,7,9]
输出: 8
```

**限制：**

```
1 <= 数组长度 <= 10000
```

```java
class Solution {
    public int missingNumber(int[] nums) {
        int k = -1;
        for(int i = 0;i < nums.length;i++)
        {
            k++;
            if(nums[i] == k)
                continue;   
            else
                return k--;
        }
        return ++k;
    }
}
```

解题思路：一一对照，当出现数字不相同的时候，该数字就是不该出现的数组。