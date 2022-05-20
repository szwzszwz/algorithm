#### [剑指 Offer 32 - I. 从上到下打印二叉树](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)

从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回：

```
[3,9,20,15,7]
```

**提示：**

1. `节点总数 <= 1000`

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
    public int[] levelOrder(TreeNode root) {
        if(root == null) // 如果树是空树，就返回空
            return new int[0];

        Queue<TreeNode> q = new LinkedList<>(); // 队列实现层序遍历
        ArrayList<Integer> array = new ArrayList<>();
        q.add(root);
        while(!q.isEmpty())
        {
            root = q.poll();
            array.add(root.val);
            if(root.left != null)
                q.add(root.left);
            if(root.right != null)
                q.add(root.right);
        }
        
        int[] tree = new int[array.size()];
        for(int i = 0;i < array.size();i++)
            tree[i] = array.get(i);

        return tree;
    }
}
```

___

#### [剑指 Offer 32 - II. 从上到下打印二叉树 II](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)

从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [9,20],
  [15,7]
]
```

**提示：**

1. `节点总数 <= 1000`

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
    public List<List<Integer>> levelOrder(TreeNode root) { // 针对List<List<Integer>>的存储方式，我们一层一层存储
        List<List<Integer>> list = new ArrayList<List<Integer>>();
        if(root == null) return list;

        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);

        while(!queue.isEmpty())
        {
            List<Integer> l = new ArrayList<Integer>();
            int size = queue.size();
            for(int i = 1;i <= size;i++)
            {
                root = queue.poll();
                l.add(root.val);
                
                if(root.left != null)
                    queue.offer(root.left);
                
                if(root.right != null)
                    queue.offer(root.right);
            
            }

            list.add(l);
        }
        return list;
    }
}
```

___

#### [剑指 Offer 32 - III. 从上到下打印二叉树 III](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [20,9],
  [15,7]
]
```

**提示：**

1. `节点总数 <= 1000`

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> list = new ArrayList<List<Integer>>();
        if(root == null) return list;

        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        int k = 1;
        while(!queue.isEmpty())
        {
            List<Integer> l = new ArrayList<Integer>();
            Stack<Integer> stack = new Stack<>(); // 使用栈的特性，反转树
            int size = queue.size();
            for(int i = 1;i <= size;i++)
            {
                if(k % 2 == 0) // 用k判断该层是否需要反转
                {
                    root = queue.poll();
                    stack.push(root.val);
                }else{
                    root = queue.poll();
                    l.add(root.val);
                }

                if(root.left != null)
                    queue.offer(root.left);
                
                if(root.right != null)
                    queue.offer(root.right);
            
            }
            if(k % 2 == 0)
                while(!stack.empty())
                    l.add(stack.pop());
        
            k++;
            list.add(l);
        }
        return list;
    }
}
```

