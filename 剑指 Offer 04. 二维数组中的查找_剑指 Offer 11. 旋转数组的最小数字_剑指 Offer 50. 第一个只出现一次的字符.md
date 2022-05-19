#### [剑指 Offer 04. 二维数组中的查找](https://leetcode.cn/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

**示例:**

现有矩阵 matrix 如下：

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

给定 target = `5`，返回 `true`。

给定 target = `20`，返回 `false`。

**限制：**

```
0 <= n <= 1000
0 <= m <= 1000
```

**方法一：**先缩小范围，再遍历整个新矩阵

```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        
        if(matrix.length == 0 || matrix[0].length == 0) // 是否为空
            return false;

        int min_x = matrix[0].length - 1,min_y = matrix.length - 1; 

        for(int i = 0;i < matrix[0].length;i++) // 根据题目给出的矩阵的性质缩小矩阵范围
            if(matrix[0][i] > target)
                min_x = i;

        for(int i = 0;i < matrix.length;i++) // 根据题目给出的矩阵的性质缩小矩阵范围
            if(matrix[i][0] > target)
                min_y = i;
        
        for(int i = 0;i <= min_x;i++)
            for(int j = 0;j <= min_y;j++) // 遍历新的矩阵，找到要找的数字
                if(matrix[j][i] == target)
                    return true;
        return false;
    }
}
```

**方法二：**从右上角开始遍历矩阵。如果当前元素等于目标值，则返回 `true`。如果当前元素大于目标值，则移到左边一列。如果当前元素小于目标值，则移到下边一行。

```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return false;
        }
        
        int rows = matrix.length, columns = matrix[0].length;
        int row = 0, column = columns - 1;
        while (row < rows && column >= 0) {
            int num = matrix[row][column];
            if (num == target) { // 如果当前元素等于目标值，则返回true
                return true;
            } else if (num > target) { // 如果当前元素大于目标值，则移到左边一列
                column--;
            } else { // 如果当前元素小于目标值，则移到下边一行
                row++;
            }
        }
        return false;
    }
}
```

___

#### [剑指 Offer 11. 旋转数组的最小数字](https://leetcode.cn/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。

给你一个可能存在 **重复** 元素值的数组 `numbers` ，它原来是一个升序排列的数组，并按上述情形进行了一次旋转。请返回旋转数组的**最小元素**。例如，数组 `[3,4,5,1,2]` 为 `[1,2,3,4,5]` 的一次旋转，该数组的最小值为 1。 

注意，数组 `[a[0], a[1], a[2], ..., a[n-1]]` 旋转一次 的结果为数组 `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]` 。

**示例 1：**

```
输入：numbers = [3,4,5,1,2]
输出：1
```

**示例 2：**

```
输入：numbers = [2,2,2,0,1]
输出：0
```

**提示：**

- `n == numbers.length`
- `1 <= n <= 5000`
- `-5000 <= numbers[i] <= 5000`
- `numbers` 原来是一个升序排序的数组，并进行了 `1` 至 `n` 次旋转

```java
class Solution {
    public int minArray(int[] numbers) {
        for(int i = 0;i < numbers.length - 1;i++)
        {
            if(numbers[i] > numbers[i + 1])
                return numbers[i + 1];
        }
        return numbers[0];
    }
}
```

解题思路：略

___

#### [剑指 Offer 50. 第一个只出现一次的字符](https://leetcode.cn/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

**示例 1:**

```
输入：s = "abaccdeff"
输出：'b'
```

**示例 2:**

```
输入：s = "" 
输出：' '
```

**限制：**

```
0 <= s 的长度 <= 50000
```

```java
class Solution {
    public char firstUniqChar(String s) {
        HashMap<Character,Boolean> dic = new HashMap<>(); // 用哈希表来判断是否存在重复的元素
        char[] sc = s.toCharArray();
        for(char c : sc) // 遍历字符串s
            dic.put(c, !dic.containsKey(c)); // 将字符串存入哈希表中，如果存在存false，如果不存在存储true
        for(char c : sc)
            if(dic.get(c))  // 遍历找到第一个true。ture为只存储一次的元素；如果存储多次，那么该元素为false
                return c;
        return ' ';   
    }
}
```

解题思路：用哈希表来判断重复。ture为只存储一次的元素；如果存储多次，那么该元素为false。