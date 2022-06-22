#### [剑指 Offer II 011. 0 和 1 个数相同的子数组](https://leetcode.cn/problems/A1NYOS/)

给定一个二进制数组 `nums` , 找到含有相同数量的 `0` 和 `1` 的最长连续子数组，并返回该子数组的长度。

**示例 1：**

~~~
输入: nums = [0,1]
输出: 2
说明: [0, 1] 是具有相同数量 0 和 1 的最长连续子数组。
~~~

**示例 2：**

~~~
输入: nums = [0,1,0]
输出: 2
说明: [0, 1] (或 [1, 0]) 是具有相同数量 0 和 1 的最长连续子数组。
~~~

**提示：**

~~~
1 <= nums.length <= 105
nums[i] 不是 0 就是 1
~~~



#### 题解：

~~~java
class Solution {
    public int findMaxLength(int[] nums) {
        int len=nums.length;
        int ans=0;
        int count=0;
        HashMap<Integer,Integer>hashMap=new HashMap<>();
        hashMap.put(0,-1);

        for(int i=0;i<len;++i){
            // 等于0时计数减少，等于1时计数增加
            if(nums[i]==0){
                count--;
            }else{
                count++;
            }
            // 哈希表中包含某个计数则代表在某区间存在相同01个数
            if(hashMap.containsKey(count)){
                // i-哈希表对应的value值即为相同01个数的区间长度
                ans=Math.max(ans,i-hashMap.get(count));
            }else{
                // 否则更新key为count对应的下标
                hashMap.put(count,i);
            }
        }
        return ans;
    }
}
~~~

