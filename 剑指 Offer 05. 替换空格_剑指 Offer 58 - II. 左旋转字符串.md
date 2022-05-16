#### [剑指 Offer 05. 替换空格](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)

请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

**示例 1：**

```
输入：s = "We are happy."
输出："We%20are%20happy."
```

**限制：**

```
0 <= s 的长度 <= 10000
```

```java
class Solution {
    public String replaceSpace(String s) {
        String ns = new String();
        for(int i = 0;i < s.length();i++)
        {
            if(s.charAt(i) == ' '){
                ns += "%20";
                continue;
            }   
            ns += s.charAt(i);
        }
       
        return ns;
    }
}
```

解题思路：利用java中的字符串拼接，当检测到空格的时候，将其替换为%20

___

#### [剑指 Offer 58 - II. 左旋转字符串](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

**示例 1：**

```
输入: s = "abcdefg", k = 2
输出: "cdefgab"
```

**示例 2：**

```
输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```

**限制：**

- `1 <= k < s.length <= 10000`

```JAVA
class Solution {
    public String reverseLeftWords(String s, int n) {
        String ns = new String();
        int k = 0;
        for(int i = n ;i < s.length();i++)
            ns += s.charAt(i);
        for(int i = 0 ;i < n;i++)
            ns += s.charAt(i);

        return ns;
    }
}
```

解题思路：创建一个新的字符串，分别将旋转位数前后的字符串放入新的数组。