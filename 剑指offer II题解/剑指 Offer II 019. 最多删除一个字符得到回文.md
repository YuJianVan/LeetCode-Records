#### [剑指 Offer II 019. 最多删除一个字符得到回文](https://leetcode.cn/problems/RQku0D/)



给定一个非空字符串 `s`，请判断如果 **最多** 从字符串中删除一个字符能否得到一个回文字符串。

**示例 1:**

```
输入: s = "aba"
输出: true
```

**示例 2:**

```
输入: s = "abca"
输出: true
解释: 可以删除 "c" 字符 或者 "b" 字符
```

**示例 3:**

```
输入: s = "abc"
输出: false
```

**提示:**

~~~
1 <= s.length <= 105
s 由小写英文字母组成
~~~



#### 题解：

~~~java
class Solution {
    public boolean validPalindrome(String s) {
        int count=1;
        int len=s.length();
        int i=0;
        int j=len-1;
        while(i<j){
            char c1=s.charAt(i);
            char c2=s.charAt(j);
            // 两指针字符相同时，正常向中心移动
            if(c1==c2){
                i++;
                j--;
            }else{
                // 两指针字符不同时，删除左边或者右边的一个字符，直接判断剩余的是否为回文即可
                return isPalindrome(i,j-1,s)||isPalindrome(i+1,j,s);
            }
        }
        return true;
    }

    public boolean isPalindrome(int i,int j,String s){
        while(i<j){
            char c1=s.charAt(i);
            char c2=s.charAt(j);
            if(c1!=c2){
                return false;
            }
            i++;
            j--;
        }
        return true;
    }
}
~~~

时间复杂度：O(n)

空间复杂度：O(1)