#### [剑指 Offer II 018. 有效的回文](https://leetcode.cn/problems/XltzEq/)

给定一个字符串 `s` ，验证 `s` 是否是 **回文串** ，只考虑字母和数字字符，可以忽略字母的大小写。

本题中，将空字符串定义为有效的 **回文串** 。



**示例 1:**

~~~
输入: s = "A man, a plan, a canal: Panama"
输出: true
解释："amanaplanacanalpanama" 是回文串
~~~

**示例 2:**

~~~
输入: s = "race a car"
输出: false
解释："raceacar" 不是回文串
~~~

**提示：**

~~~
1 <= s.length <= 2 * 105
字符串 s 由 ASCII 字符组成
~~~



#### 题解：

1. 双指针

   ~~~java
   class Solution {
       public boolean isPalindrome(String s) {
           String str=preProcess(s);
           // 双指针判断是否是回文
           int i=0;
           int j=str.length()-1;
           while(i<j&&str.charAt(i)==str.charAt(j)){
               i++;
               j--;
           }
           return j<=i;
       }
   	
       // 将字符串进行预处理，只保留字符和数字
       public String preProcess(String s){
           StringBuilder strBuilder=new StringBuilder();
           int len=s.length();
           for(int i=0;i<len;++i){
               char c=s.charAt(i);
               if(Character.isDigit(c)||Character.isLetter(c)){
                   strBuilder.append(c);
               }
           }
           return strBuilder.toString().toLowerCase();
       }
   }
   ~~~

   时间复杂度：O(n)  n=字符串长度

   空间复杂度：O(n)	需要额外的空间存储字符串

   

2. 反转字符串，判断是否一样

   ~~~java
   class Solution {
       public boolean isPalindrome(String s) {
           StringBuilder strBuilder=new StringBuilder();
           int len=s.length();
           for(int i=0;i<len;++i){
               char c=s.charAt(i);
               if(Character.isLetterOrDigit(c)){
                   strBuilder.append(Character.toLowerCase(c));
               }
           }
           // 反转字符串，若反转前后相等，则为回文字符串
           StringBuilder strBuilder2=new StringBuilder(strBuilder).reverse();
           return strBuilder.toString().equals(strBuilder2.toString());
       }
   }
   ~~~

   时间复杂度：O(n)  n=字符串长度

   空间复杂度：O(n)	需要额外的空间存储字符串