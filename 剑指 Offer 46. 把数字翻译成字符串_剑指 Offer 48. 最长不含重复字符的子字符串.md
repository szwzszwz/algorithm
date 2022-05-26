#### [剑指 Offer 46. 把数字翻译成字符串](https://leetcode.cn/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

**示例 1:**

```
输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
```

**提示：**

- `0 <= num < 231`

```java
class Solution {
    public int translateNum(int num) {
        String s = String.valueOf(num);
        int a = 1,b = 1;
        for(int i = 2;i <= s.length();i++)
        {
            String tmp = s.substring(i - 2, i);
            int c = tmp.compareTo("10") >= 0 && tmp.compareTo("25") <= 0 ? a + b : a;
            b = a;
            a = c;
        }
        return a;
    }
}
```

解题思路：斐波那契数列。动态规划转移方程为：`f(i) = f(i − 1) + f(i − 2),其中[i − 1 ≥ 0,10 ≤ x 25]`

如果在10~25之间，那么意味着执行斐波那契累加，如果没有在这个范围内，那么不变。

___

#### [剑指 Offer 48. 最长不含重复字符的子字符串](https://leetcode.cn/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)

请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

**示例 1:**

```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**

```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

**示例 3:**

```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

提示：

- `s.length <= 40000`

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
 		int n = s.length(),ans = 0;
        Map<Character,Integer> map = new HashMap<>();
        for(int end = 0,start = 0;end < n;end++)
        {
            char alpha = s.charAt(end);
            
            if(map.containsKey(alpha))
                start = Math.max(map.get(alpha),start); // 当该字母出现过，用来移动start指针
           	
            ans = Math.max(ans,end - start + 1); // 遍历的过程中，用来记录最大长度
            map.put(s.charAt(end),end + 1); // 用来记录字母重复的时候移动到的位置
        }
        return ans;
    }
}
```

解题思路：用哈希表来判断字母是否出现过。如果出现过更新start指针的位置，如果没有出现过end指针继续向后寻找。