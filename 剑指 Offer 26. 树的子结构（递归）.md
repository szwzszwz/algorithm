#### [剑指 Offer 26. 树的子结构](https://leetcode.cn/problems/shu-de-zi-jie-gou-lcof/)

输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如:
给定的树 A:

```
     3
    / \
   4   5
  / \
 1   2
```

给定的树 B：

```
   4 
  /
 1
```

返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。

**示例 1：**

```
输入：A = [1,2,3], B = [3,1]
输出：false
```

**示例 2：**

```
输入：A = [3,4,5,1,2], B = [4,1]
输出：true
```

**限制：**

```
0 <= 节点个数 <= 10000
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
   public boolean isSubStructure(TreeNode A, TreeNode B) {
       // 用来遍历A树，直到找到对应的第一个结点
		return (A != null && B != null) && (recur(A,B) || isSubStructure(A.left,B) || isSubStructure(A.right,B));   // isSubStructure(A.left,B) || isSubStructure(A.right,B)这个遍历树的顺序是DFS
   }

    boolean recur(TreeNode A, TreeNode B) {
		if(B == null) return true; // 当B树结束的时候，说明为子结构
        if(A == null || A.val != B.val) return false; // 当A找完且B没有找完，或者没有找到两个树的相同结点
        
        return recur(A.left,B.left) && recur(A.right,B.right); // 当A、B不为空，且找到对应的点相同的时候
    }
}
```

解题思路：递归遍历A树的所有节点，当找到A的一个节点与B的根节点相同时，同时遍历两棵树。

B树结束的时候说明B是A的子结构。

___

#### [剑指 Offer 27. 二叉树的镜像](https://leetcode.cn/problems/er-cha-shu-de-jing-xiang-lcof/)

请完成一个函数，输入一个二叉树，该函数输出它的镜像。

例如输入：

 ```
      4
    /   \
   2     7
  / \   / \
 1   3 6   9
 ```


镜像输出：

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

**示例 1：**

```
输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]
```

**限制**

```
0 <= 节点个数 <= 1000
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
    public TreeNode mirrorTree(TreeNode root) {
        if(root == null) return root;
        TreeNode left = mirrorTree(root.left);
        TreeNode right = mirrorTree(root.right);

        root.left = right;
        root.right = left;

        return root;
    }
}
```

解题思路：二叉树只需要两两交换即可。DFS

```
     4
   /   \
  2     7       ===>  
 / \   / \
1   3 6   9 

     4
   /   \
  2     7       ===>    
 / \   / \
3   1 6   9

     4
   /   \
  2     7       ===>    
 / \   / \
3   1 9   6

     4
   /   \
  7     2       结束！   
 / \   / \
9   6 3   1
```

___

#### [剑指 Offer 28. 对称的二叉树](https://leetcode.cn/problems/dui-cheng-de-er-cha-shu-lcof/)

请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

```
    1
   / \
  2   2
   \   \
   3    3
```

**示例 1：**

```
输入：root = [1,2,2,3,4,4,3]
输出：true
```

**示例 2：**

```
输入：root = [1,2,2,null,3,null,3]
输出：false
```

**限制：**

```
0 <= 节点个数 <= 1000
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
    public boolean isSymmetric(TreeNode root) {
        return check(root, root);
    }

    public boolean check(TreeNode p, TreeNode q) {
        if (p == null && q == null) { // 同时为空，对称！
            return true;
        }
        if (p == null || q == null) { // 不同时为空，不对称！
            return false;
        }
        return p.val == q.val && check(p.left, q.right) && check(p.right, q.left); // check(p.left, q.right) && check(p.right, q.left) 这个遍历树的顺序是DFS
    }
}
```

解题思路：两个相同的树，一个向左边遍历，一个向右边遍历。但两个树同时为空且两个树对应的点完全相同，那么说明对称！（根据二叉树的对称性）。DFS