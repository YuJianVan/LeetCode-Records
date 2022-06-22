#### [剑指 Offer II 014. 字符串中的变位词](https://leetcode.cn/problems/MPnaiL/)

给定两个字符串 `s1` 和 `s2`，写一个函数来判断 `s2` 是否包含 `s1` 的某个变位词。

换句话说，第一个字符串的排列之一是第二个字符串的 **子串** 。

**示例 1：**

~~~
输入: s1 = "ab" s2 = "eidbaooo"
输出: True
解释: s2 包含 s1 的排列之一 ("ba").
~~~

**示例 2：**

~~~
输入: s1= "ab" s2 = "eidboaoo"
输出: False
~~~

**提示：**

~~~
1 <= s1.length, s2.length <= 104
s1 和 s2 仅包含小写字母
~~~



#### 题解

滑动窗口：保持窗口长度等于s1长度，在s2上右移窗口。存在子串的依据是存放字符串的数组相同

~~~java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        int len1=s1.length();
        int len2=s2.length();
        // 题目要求判断s1是否是s2的子串，所以s1长度大于s2直接返回false
        if(len1>len2){
            return false;
        }

        int[] arr1=new int[26];
        int[] arr2=new int[26];

        for(int i=0;i<len1;++i){
            arr1[s1.charAt(i)-'a']++;
            arr2[s2.charAt(i)-'a']++;
        }
        // 判断前len1个长度下两个字符串是否相等
        if(Arrays.equals(arr1,arr2)){
            return true;
        }

        for(int j=len1;j<len2;++j){
            // 窗口大小保持len1不变，右边向右移动，左边收缩
            arr2[s2.charAt(j-len1)-'a']--;
            arr2[s2.charAt(j)-'a']++;
            if(Arrays.equals(arr1,arr2)){
                return true;
            }
        }
        return false;

    }
}
~~~

