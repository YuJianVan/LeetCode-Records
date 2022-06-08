给你一个整数数组 nums ，除某个元素仅出现 一次 外，其余每个元素都恰出现 三次 。请你找出并返回那个只出现了一次的元素。

 

~~~java
示例 1：

输入：nums = [2,2,3,2]
输出：3
    
示例 2：

输入：nums = [0,1,0,1,0,1,100]
输出：100
~~~

提示：

~~~java
1 <= nums.length <= 3 * 104
-231 <= nums[i] <= 231 - 1
nums 中，除某个元素仅出现 一次 外，其余每个元素都恰出现 三次
~~~


进阶：你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

1. HashMap

~~~java
class Solution {
    public int singleNumber(int[] nums) {
        int len=nums.length;
        HashMap<Integer,Integer>hashMap=new HashMap<>();
        for(int i=0;i<len;++i){
            hashMap.put(nums[i],hashMap.getOrDefault(nums[i],0)+1);
        }
        for(int n:hashMap.keySet()){
            if(hashMap.get(n)==1){
                return n;
            }
        }
        return -1;
    }
}
~~~

时间复杂度：O(n)  n=nums.length

空间复杂度：O(n)   



2. 位运算

~~~java
class Solution {
    public int singleNumber(int[] nums) {
        int ans=0;
        for(int i=0;i<32;++i){
            int temp=0;
            for(int n:nums){
                temp+=((n>>i)&1);
            }
            if(temp%3!=0){
                ans|=(1<<i);
            }
        }
        return ans;
    }
}
~~~

时间复杂度：O(nlogC)

空间复杂度：O(1)

