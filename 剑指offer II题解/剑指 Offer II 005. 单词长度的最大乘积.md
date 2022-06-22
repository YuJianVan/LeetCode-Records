#### [剑指 Offer II 005. 单词长度的最大乘积](https://leetcode.cn/problems/aseY1I/)

给定一个字符串数组 words，请计算当两个字符串 words[i] 和 words[j] 不包含相同字符时，它们长度的乘积的最大值。假设字符串中只包含英语的小写字母。如果没有不包含相同字符的一对字符串，返回 0。

**示例 1:**

~~~
输入: words = ["abcw","baz","foo","bar","fxyz","abcdef"]
输出: 16 
解释: 这两个单词为 "abcw", "fxyz"。它们不包含相同字符，且长度的乘积最大。
~~~

**示例 2:**

~~~java
输入: words = ["a","ab","abc","d","cd","bcd","abcd"]
输出: 4 
解释: 这两个单词为 "ab", "cd"。
~~~

**示例 3:**

~~~java
输入: words = ["a","aa","aaa","aaaa"]
输出: 0 
解释: 不存在这样的两个单词。
~~~

**提示：**

~~~java
2 <= words.length <= 1000
1 <= words[i].length <= 1000
words[i] 仅包含小写字母
~~~



##### 思路：

利用字母最多只有26个，但int整型有32位的特点，每种字母占用一个整数的一位，通过位运算中的&与运算判定是否重复

~~~java
class Solution {
    public int maxProduct(String[] words) {
        int len=words.length;
        HashMap<Integer,Integer>hashMap=new HashMap<>();
        for(int i=0;i<len;++i){
            int l=words[i].length();  // 字符串长度
            int bitmark=0;
            // 遍历字符串，将其转换成对应位置的1
            for(int j=0;j<l;++j){	
                bitmark|=(1<<(words[i].charAt(j)-'a'));
            }
            // value值为最大长度
            hashMap.put(bitmark,Math.max(l,hashMap.getOrDefault(bitmark,0)));
        }

        int ans=0;
        for(int i:hashMap.keySet()){
            for(int j:hashMap.keySet()){
                // 根据与预算特点，相与为0代表没有重复
                if((i&j)==0){
                    ans=Math.max(ans,hashMap.get(i)*hashMap.get(j));
                }
            }
        }
        return ans;
    }
}
~~~

时间复杂度：O(m*n+n^2)

空间复杂度：O(n)