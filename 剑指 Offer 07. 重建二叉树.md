#### [剑指 Offer 07. 重建二叉树](https://leetcode.cn/problems/zhong-jian-er-cha-shu-lcof/)

输入某二叉树的前序遍历和中序遍历的结果，请构建该二叉树并返回其根节点。

假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

**示例 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

**示例 2:**

```
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```

**限制：**

```
0 <= 节点个数 <= 5000
```

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    int[] preorder;
    HashMap<Integer, Integer> dic = new HashMap<>();

    public TreeNode buildTree(int[] preorder, int[] inorder) {
        this.preorder = preorder;
        for(int i = 0;i < inorder.length;i++)
            dic.put(inorder[i],i); 
         return recur(0,0,inorder.length - 1);
    }

    TreeNode recur(int root, int left, int right) {
        if(left > right) return null;                          // 递归终止

        TreeNode node = new TreeNode(preorder[root]);          // 建立根节点
        
        int i = dic.get(preorder[root]);                       // 划分根节点、左子树、右子树
        
        node.left = recur(root + 1, left, i - 1);              // 开启左子树递归
        node.right = recur(root + i - left + 1, i + 1, right); // 开启右子树递归
        
        return node;                                           // 回溯返回根节点
    }
}
```

解题思路：

递推参数： 根节点在**前序遍历**的索引 `root `、子树在**中序遍历**的左边界 `left `、子树在**中序遍历**的右边界 `right` ；

终止条件： 当` left > right` ，代表已经越过叶节点，此时返回 `null` ；

递推工作：

+ 建立根节点` node` ： 节点值为 `preorder[root] `；
+ 划分左右子树： 查找根节点在中序遍历` inorder` 中的索引 `i` ；
+ 为了提升效率，本文使用哈希表 `dic` 存储中序遍历的值与索引的映射，查找操作的时间复杂度为` O(1)` ；
+ 构建左右子树： 开启左右子树递归；

|        | 根节点索引                                                   | 中序遍历左边界                                               | 中序遍历右边界                                               |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 左子树 | `root + 1`（表示<u>根节点的左子树的根节点位置</u>为当前根节点位置+1） | `left`（表示根节点左子树的最左结点）                         | `i - 1`（表示根节点左子树的最右结点===>即根节点-1，其中i表示为中序遍历中根节点的位置） |
| 右子树 | `i - left + root + 1`（表示<u>根节点的右子树的根节点位置</u>为当前根节点位置+当前根节点的左子树大小+1） | `i + 1`（表示根节点右子树的最左结点===>即根节点+1，其中i表示为中序遍历中根节点的位置） | `right`（表示根节点右子树的最右结点）                        |

TIPS： `i - left + root + 1`含义为 `左子树长度 + 根节点索引 + 1`

注释：**根节点索引**表示在**前序遍历**中根节点的位置，会根据分治算法进入不同的子树，找到各个子树中的根节点。

___

举例：

```
    1
   / \
  2   3
 /\   /\
4  5 6  7

先序遍历   preorder = [1,2,4,5,3,6,7]
中序遍历   inorder = [4,2,5,1,6,3,7]
```

（注：加粗为根节点，下划线为左子树，斜体为右子树,`i`表示为中序遍历中根节点的位置）

**根节点：**先序遍历[**1**,<u>2,4,5</u>,*3,6,7*]   ==>  中序遍历 [<u>4,2,5</u>,**1**,*6,3,7*]   ==>  i = 3

**左子树：**先序遍历[1,**2**,4,5,3,6,7]` (root + 1 = 0 + 1 = 1) ` ==>  中序遍历 [<u>4</u>,**2**,*5*,1,6,3,7] `(left = 0,right = i - 1) ` ==>  i = 1  ==>  在对左右子树进行递归调用。。。  

**右子树：**先序遍历[1,2,4,5,**3**,6,7] `(root + 1 + i - left = 0 + 1 + 3 - 0 = 4) ` ==>  中序遍历 [4,2,5,1,<u>6</u>,**3**,*7*]`（left = i + 1,right = preorder.length）`   ==>  i =  5  ==>  在对左右子树进行递归调用。。。  



***由于使用hashmap本方法只适用于 “无重复节点值” 的二叉树。***









先序遍历[1,**2**,4,5,3,6,7]   ==>  中序遍历 [4,2,5,1,6,3,7]   ==>  i = 0

先序遍历[1,**2**,4,5,3,6,7]   ==>  中序遍历 [4,2,5,1,6,3,7]   ==>  i = 0

先序遍历[1,**2**,4,5,3,6,7]   ==>  中序遍历 [4,2,5,1,6,3,7]   ==>  i = 0