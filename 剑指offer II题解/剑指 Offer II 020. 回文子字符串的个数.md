#### [剑指 Offer II 020. 回文子字符串的个数](https://leetcode.cn/problems/a7VOhD/)

给定一个字符串 `s` ，请计算这个字符串中有多少个回文子字符串。

具有不同开始位置或结束位置的子串，即使是由相同的字符组成，也会被视作不同的子串。

**示例 1：**

```
输入：s = "abc"
输出：3
解释：三个回文子串: "a", "b", "c"
```

**示例 2：**

```
输入：s = "aaa"
输出：6
解释：6个回文子串: "a", "a", "a", "aa", "aa", "aaa"
```

**提示：**

- `1 <= s.length <= 1000`
- `s` 由小写英文字母组成



#### 题解

思路：遍历每一个元素，假定为回文字符串中心字符，回文字符串分为两种情况：

1. 长度为奇数   如  abcba
2. 长度为偶数    如 abccba

因此算上两种情况的回文字符串个数之和，即为结果

~~~java
class Solution {
    int len;
    public int countSubstrings(String s) {
        this.len=s.length();
        int ans=0;
        for(int i=0;i<len;++i){
            ans+=count(s,i,i); // 左右坐标相同，对应长度为奇数的回文串
            ans+=count(s,i,i+1);  // 左右坐标不同，对应长度为偶数的回文串
        }
        return ans;
    }
    /**
        传入起始坐标，向两侧扩散
     */
    public int count(String s,int i,int j){
        int res=0;
        while(i>=0&&j<len&&s.charAt(i)==s.charAt(j)){
            i--;
            j++;
            res++;
        }
        return res;
    }
}
~~~

时间复杂度：O(n^2)

空间复杂度：O(1)