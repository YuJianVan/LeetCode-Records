#### [剑指 Offer II 008. 和大于等于 target 的最短子数组](https://leetcode.cn/problems/2VG8Kg/)

给定一个含有 n 个正整数的数组和一个正整数 target 。

找出该数组中满足其和 ≥ target 的长度最小的 连续子数组 [numsl, numsl+1, ..., numsr-1, numsr] ，并返回其长度。如果不存在符合条件的子数组，返回 0 。



**示例 1：**

~~~
输入：target = 7, nums = [2,3,1,2,4,3]
输出：2
解释：子数组 [4,3] 是该条件下的长度最小的子数组。
~~~

**示例 2：**

~~~
输入：target = 4, nums = [1,4,4]
输出：1
~~~

**示例 3：**

~~~
输入：target = 11, nums = [1,1,1,1,1,1,1,1]
输出：0
~~~

提示：

~~~
1 <= target <= 109
1 <= nums.length <= 105
1 <= nums[i] <= 105
~~~


进阶：

如果你已经实现 O(n) 时间复杂度的解法, 请尝试设计一个 O(n log(n)) 时间复杂度的解法。



#### 解答

滑动窗口：长度为右指针-左指针+1

~~~java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int len=nums.length;    // 数组长度
        int sum=0;  // 滑动窗口内元素之和
        int i=0; // 左指针
        int j=0; // 右指针
        int ans=Integer.MAX_VALUE; // 最短长度
        while(j<len){
            // 窗口向右扩展
            sum+=nums[j];
            // 满足要求后取最短区间j-i+1，并收缩左侧窗口
            while(sum>=target){
                ans=Math.min(ans,j-i+1);
                sum-=nums[i];
                i++;
                // 此处通过sum的值确保了i不会大于j
            }
            j++;
        }
        return ans==Integer.MAX_VALUE?0:ans;
    }
}
~~~

时间复杂度：O(n)

空间复杂度：O(1)



前缀和+二分查找

~~~java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int len=nums.length;    // 数组长度
        int ans=Integer.MAX_VALUE; // 最短长度
        // 前缀和数组
        int[] sum=new int[len+1];
        for(int i=1;i<len+1;++i){
            sum[i]=sum[i-1]+nums[i-1];
        }

        // 二分查找
        for(int i=1;i<len+1;++i){
            int bound=Arrays.binarySearch(sum,target+sum[i-1]);
            if(bound<0){
                bound=-(bound+1);  // 由于binarySearch中没找到会返回-(low+1)，因此此处取反，获得恰好大于目标的下标
            }
            if(bound<=len){
                ans=Math.min(ans,bound-(i-1));  // 区间长度=bound-(i-1)
            }
        }
        return ans==Integer.MAX_VALUE?0:ans;
    }
}
~~~

时间复杂度：O(nlogn)

分析：二分查找时间复杂度为O(logn)，遍历前缀和数组时间复杂度为O(n)，综合为O(nlogn)

空间复杂度：O(n)

分析：前缀和数组存储了数据，空间复杂度为O(n)