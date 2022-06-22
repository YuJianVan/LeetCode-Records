#### [剑指 Offer II 015. 字符串中的所有变位词](https://leetcode.cn/problems/VabMRr/)

给定两个字符串 s 和 p，找到 s 中所有 p 的 变位词 的子串，返回这些子串的起始索引。不考虑答案输出的顺序。

变位词 指字母相同，但排列不同的字符串。



**示例 1：**

~~~
输入: s = "cbaebabacd", p = "abc"
输出: [0,6]
解释:
起始索引等于 0 的子串是 "cba", 它是 "abc" 的变位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的变位词。
~~~

**示例 2：**

~~~
输入: s = "abab", p = "ab"
输出: [0,1,2]
解释:
起始索引等于 0 的子串是 "ab", 它是 "ab" 的变位词。
起始索引等于 1 的子串是 "ba", 它是 "ab" 的变位词。
起始索引等于 2 的子串是 "ab", 它是 "ab" 的变位词。
~~~

**提示:**

~~~
1 <= s.length, p.length <= 3 * 104
s 和 p 仅包含小写字母
~~~



#### 题解：

滑动窗口：思路参考上一题

~~~java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer>list=new ArrayList<>();
        int len1=s.length();
        int len2=p.length();
        if(len1<len2){
            return list;
        }

        int[] s1=new int[26];
        int[] s2=new int[26];

        for(int i=0;i<len2;++i){
            s2[p.charAt(i)-'a']++;
            s1[s.charAt(i)-'a']++;
        }
        if(Arrays.equals(s1,s2)){
            list.add(0);
        }

        for(int i=len2;i<len1;++i){
            s1[s.charAt(i-len2)-'a']--;
            s1[s.charAt(i)-'a']++;
            if(Arrays.equals(s1,s2)){
                list.add(i-len2+1);
            }
        }
        return list;

    }
}
~~~

